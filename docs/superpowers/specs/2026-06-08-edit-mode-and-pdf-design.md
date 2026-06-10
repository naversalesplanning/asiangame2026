# 수정모드 + PDF 다운로드 — 설계 문서

작성일: 2026-06-08 · 대상 파일: `index.html` (단일 HTML)

## 목표
1. 비개발자가 코드 편집 없이 슬라이드 **텍스트 + 이미지**를 바로 고칠 수 있는 **수정모드** 추가
2. 인쇄 대화상자 없이 **원클릭으로 진짜 PDF 파일**을 다운로드하는 기능 추가 (기존 인쇄 버튼은 제거)

## 결정 사항 (사용자 확정)
- 편집 범위: **텍스트 + 이미지**
- 저장: **브라우저 저장만** (이 브라우저에만 유지, 배포본/타 PC 미반영)
- PDF: **원클릭 진짜 PDF 다운로드** (`html2canvas` + `jsPDF`)
- 버튼: PDF는 **다운로드 버튼 1개만** (인쇄 버튼 제거)

## 1. 수정모드
- 진입점: 좌하단 툴바에 `✏️ 수정` 버튼 (게이트 해제 후 노출, 프리젠테이션 중 숨김). 단축키 `E`.
- 토글 시 `body.editing` 클래스 + 상단 노란 배너("수정모드 ON — 텍스트 클릭해 편집, 이미지 클릭해 교체").
- 프리젠테이션 진입 시 수정모드 자동 해제(MutationObserver 감시).

### 텍스트 편집
- 문서 순서대로 **말단 텍스트 요소**(자식 요소가 없거나 `<br>`만 있고, 공백 아닌 텍스트 보유)에 `data-eid` 부여.
- 제외: `<script>/<style>/<svg>/<button>/<input>` 및 SVG 내부, 이미지 placeholder(`.ph-fallback`,`.cover-ph-fallback`).
- 수정모드일 때만 해당 요소에 `contenteditable=true`. 호버 점선 / 포커스 골드 아웃라인.
- 한계(허용): `<em>`,`<b>` 등 인라인 자식을 가진 혼합 요소는 통째 편집 대신 인라인 조각만 개별 편집됨.

### 이미지 편집
- 대상: `img.mock-img`, `img.aichi-logo` (NAVER 로고는 제외). 각 부모에 `data-ieid` 부여 + 클릭 핫스팟.
- 수정모드 클릭 → 파일 선택 → DataURL 읽어 `img.src` 교체 + `no-img` 클래스 제거(placeholder 가림).

## 2. 저장 (브라우저)
- 텍스트: `localStorage["nag-edit-text-v1"]` = `{ eid: innerHTML }`. input 이벤트 시 디바운스(400ms) 저장.
- 이미지: **IndexedDB**(`nag-edits`/store `img`) = `{ ieid: dataURL }` (localStorage 용량 한계 회피).
- 로드 시 텍스트 복원은 **카운터 애니메이션 초기화보다 먼저** 실행 → 수정된 숫자도 카운터가 그 값으로 애니메이션.
- `↺ 초기화` 버튼: 확인 후 localStorage 키 삭제 + IndexedDB clear + reload.
- 키(eid/ieid)는 문서 순서 기반 → HTML 구조가 동일한 한 새로고침/재배포에도 안정적으로 매핑.

## 3. 원클릭 PDF
- 기존 `#pdfBtn` 핸들러(`window.print()`) 제거 → 원클릭 다운로드로 교체.
- 라이브러리는 클릭 시 CDN에서 **지연 로드**(초기 로딩/오프라인 편집 영향 없음).
- 18개 `.slide`를 각각 `html2canvas`(scale 2, useCORS, width 1600 × height 900)로 렌더 → A4 가로 PDF에 16:9 비율 유지 배치(레터박스) → `2026_AsianGames_AichiNagoya_NaverPremium.pdf` 저장.
- 진행률 버튼 라벨 표시("PDF 생성 중 5/18…"). 생성 전 수정모드/프리젠테이션 해제.

## 트레이드오프 / 주의
- **CORS**: 외부 CDN 이미지(위키미디어 NAVER 로고 등)가 CORS를 막으면 PDF에서 빈칸 가능. 실패 시 `Cmd/Ctrl+P → PDF로 저장` 폴백 안내(alert).
- **브라우저 한정 저장**: GitHub Pages 배포본·다른 기기엔 반영 안 됨(사용자 선택).
- **혼합 텍스트 요소**: 인라인 자식이 섞인 요소는 조각 단위 편집(상기).

## 인쇄/프리젠테이션 정합성
- 배너·편집 아웃라인은 `@media print` 및 `body.presenting`에서 숨김.
- 수정모드 클릭이 표지/마지막장 confetti와 충돌하지 않도록 confetti 핸들러에 `!editing` 가드 추가.

## 개정 (2026-06-08, 후속 요청)
사용자 후속 요청으로 두 가지 변경:

### A. 수정모드 시크릿화 (URL 키)
- 수정/내보내기/초기화 버튼은 기본 `display:none`. URL에 `?edit=nag-edit`(또는 `#nag-edit`)가 있을 때만 `body.edit-enabled`를 부여해 노출하고 `E`키 단축키도 그때만 활성화. 키 상수 `EDIT_KEY='nag-edit'`.
- 광고주/일반 사용자는 버튼 존재 자체를 모름. 편집 권한자만 URL로 진입.

### B. 배포용 HTML 내보내기 (편집 내용 bake)
- 처음의 "브라우저 저장만"으로는 편집이 파일에 안 담겨 배포 불가임을 사용자에게 설명 → 내보내기 추가.
- `💾 배포용 저장` 버튼(수정모드일 때만 노출): 현재 DOM을 복제해 편집 흔적(`contenteditable`/`editing`/`presenting`/`edit-enabled`)과 숨김 파일입력·지연로드 라이브러리 스크립트를 제거하고 `<!doctype>`를 붙여 `index.html`로 다운로드. 텍스트·교체 이미지(data URL)가 파일 내부에 그대로 포함됨.
- **배포 반영 경로**: `💾 배포용 저장`으로 받은 index.html을 git에 push → GitHub Pages에서 모두가 편집본 열람. (localStorage/IndexedDB는 파일에 안 담기므로 push 대상 아님.)
