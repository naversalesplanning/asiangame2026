# 2026 아이치-나고야 아시안게임 세일즈덱 · 작업 내역

> 이 문서는 Claude와의 대화로 진행된 모든 주요 변경/결정 사항을 정리한 워크로그입니다.
> 마지막 업데이트: 2026-07-13

---

## 🎯 프로젝트 개요

- **목표**: 2026 아이치-나고야 아시안게임 NAVER 광고 패키지 세일즈덱 제작 (HTML 단일 파일)
- **베이스**: `/Users/user/Documents/SalesDeck_WORLDCUP/(공통)NAVER_2026월드컵_프리미엄패키지.pptx` 구성을 참고
- **데이터**: `/Users/user/Documents/salesdeck_asiangame/` 의 4개 항저우 아시안게임 PDF + 항저우 검색 지식베이스 PDF
- **배포**: GitHub Pages (https://naversalesplanning.github.io/asiangame2026/)
- **보안**: 콘텐츠 암호화(AES-256-GCM). 비밀번호 `nasiangame2026`이 복호화 키 — 소스에 단가 평문 없음 (Session 7)

---

## 📁 파일 구조

```
/Users/user/Documents/salesdeck_asiangame/
├── index.html                                    # 메인 파일 (GitHub Pages 진입점)
├── 2026_AsianGames_AichiNagoya_NaverPremium.html # 로컬 백업 (.gitignore)
├── README.md
├── .gitignore                                    # PDF/PPTX 제외
├── claude.md                                     # ← 이 파일
├── images/                                       # 이미지 플레이스홀더 폴더
│   ├── .gitkeep
│   ├── cover-emblem.png                          # (직접 추가 필요)
│   ├── slide07-feature-mobile.png · slide07-feature-pc.png
│   ├── slide07-chzzk-pc.png · slide07-chzzk-mobile.png
│   ├── slide09-special-template.png
│   ├── slide10-story-1.png · slide10-story-main.png · slide10-story-3.png
│   ├── slide11-pc-sideskin.png · slide11-mo-banner.png
│   └── slide14-pc.png · slide14-phone.png
└── (PDFs — git에 안 올라감, 로컬 confidential)
    ├── (NAVER)항저우 아시안게임 광고 상품 소개서_농구배구.pdf
    ├── (NAVER)항저우 아시안게임 광고 상품 소개서_아시안게임.pdf
    ├── (NAVER)항저우 아시안게임 광고 상품 소개서_야구독점.pdf
    ├── (NAVER)항저우 아시안게임 광고 상품 소개서_축구독점.pdf
    └── 항저우아시안게임 지식베이스 검색 지표_20231010.pdf
```

---

## 🗂 슬라이드 구성 (총 18장)

| # | 슬라이드 | 비고 |
|---|---|---|
| 01 | 표지 | Aichi-Nagoya 로고 placeholder + 20th Asian Games / Aichi-Nagoya 2026 |
| 02 | 대회 · 광고 정보 | 좌측 일정/정보, 우측 트래픽 KPI 4종 |
| 03 | Why Naver | "아시안 게임의 모든 순간, NAVER에서 만나는, IMAGINE ONE ASIA" 3줄 + 박싱 4 reasons |
| 04 | 광고 기회의 가치 | SCALE/STARS/TIME/GOAL 4 카드 (큰 박스 뱃지 제거됨) |
| 05 | 한국 대표팀 일정 | 9개 이벤트: 개막·양궁·사격·펜싱·축구한일전·태권도·e스포츠·야구·폐막 |
| 06 | 항저우 실 KPI 9-grid | 1.77억 QC / 신유빈 191만 / 페이커 46만 등 PDF 8/9 직접 인용 |
| 07 | NAVER × 아시안게임 시너지 | 특집페이지 + 치지직 모형 (이미지 placeholder) |
| **08** | **DIVIDER · CHAPTER 01 · 패키지 구성** | (재배치 후 패키지가 먼저) |
| 09 | 5-tier 패키지 그리드 | GOLD/SILVER/BRONZE/FINALIST/OPENER · 메달 그라데이션 헤더 |
| 10 | GOLD 패키지 상세 | 좌 다크 패널 + 우 디바이스 목업 + 4 카테고리 |
| 11 | GOLD 단가표 | 13항목 + TOTAL + 판매가 |
| 12 | 종목 특화 패키지 | 축구/야구/농구&배구 3 카드 |
| **13** | **DIVIDER · APPENDIX · 상품 소개** | (Chapter 01 → APPENDIX로 변경) |
| 14 | [메인] 스페셜 템플릿 | 모바일 폰 목업 |
| 15 | [스포츠] 브랜드 트렌드 스토리 | 3 미니폰 목업 |
| 16 | [스포츠] PC 사이드스킨 / MO 띠배너 | 랩탑 + 미니폰 |
| 17 | 유의사항 | 8개 노트 카드 |
| 18 | E.O.D. (감사합니다) | 월드컵 데크 포맷 — 빨강 배경 + NAVER + Aichi 로고 + 문의 DL |

---

## 🎨 디자인 결정

### 컬러 팔레트 (2026 아이치-나고야 공식 사이트 CSS에서 직접 추출)
| 변수 | 값 | 용도 |
|---|---|---|
| `--gold` | `#d5b200` | 시그니처 골드 (사이트 최다 사용 컬러) |
| `--gold-bright` | `#FFEC8D` | 밝은 크림 옐로우 |
| `--accent-red` | `#BF0D0D` | 딥 레드 |
| `--green` (== red mapped) | `#d2372f` | 브랜드 레드 (강조 액션) |
| `--purple` | `#4e3a93` | 멀티컬러 액센트 |
| `--teal` | `#19aea9` · `#4cc0bc` | 멀티컬러 액센트 |
| `--green-asia` | `#07993F` | 멀티컬러 액센트 |
| `--orange` · `--coral` | `#e87e20` · `#FE6152` | 멀티컬러 액센트 |
| `--ink` | `#322d2a` | 다크 웜 베이스 |

### 폰트
- **나눔스퀘어 네오** (NAVER 공식 한글 폰트)
- CDN: `https://cdn.jsdelivr.net/gh/fonts-archive/NanumSquareNeo/NanumSquareNeo.css`
- font-family: `'Nanum Square Neo'` (공백 포함!)
- weights: 300/400/700/800/900
- ⚠️ 잘못된 CDN URL 시행착오 4회: hangeul.pstatic.net, projectnoonnu, webfontworld 모두 404 → fonts-archive 검증으로 해결

### NAVER 로고
- 초록 NAVER: Wikipedia Commons SVG PNG (`upload.wikimedia.org/wikipedia/commons/thumb/2/23/Naver_Logotype.svg/3840px-Naver_Logotype.svg.png`)
- 흰색 NAVER (s18 상단): freebiesupply PNG + `filter:brightness(0) invert(1)`
- 위치: 표지 / s18만 노출 (`.slide .brand-mark{display:none}` 전역 + `#s18 .brand-mark{display:inline-flex}` 예외)

---

## 🛠 기술 결정

### 컨테이너 쿼리
- `.slide{container-type:inline-size;container-name:slide}`
- 모든 슬라이드 내부 폰트사이즈를 `cqw` (1% of slide width)로 통일
- 이유: 프리젠테이션 모드와 스크롤 모드에서 텍스트 비율 동일 유지

### 프리젠테이션 모드
- 좌하단 ▶ 프리젠테이션 버튼 또는 키보드 F
- Fullscreen API + `body.presenting` 클래스 토글
- 슬라이드 1600×900 고정 + flex 센터링 + `transform:scale(min(100vw/1600, 100vh/900))`
- ESC로 종료, ←/→/Space로 이동, Home/End로 처음/끝
- ⚠️ 시행착오: translate(-50%,-50%) scale로 했더니 % 계산 버그 / 100vw 100vh로 했더니 absolute 배치 레이아웃 깨짐 → 최종 16:9 strict + flex 센터링

### 인쇄 / PDF
- `@page{size:297mm 210mm;margin:0}` A4 가로 강제
- `print-color-adjust:exact` 전역 적용 → 다크 배경/그라데이션/브랜드 컬러 모두 컬러 인쇄
- PDF 버튼이 프리젠테이션 모드 자동 종료 후 호출 (18장 모두 포함)

### 비밀번호 게이트
- 클라이언트 사이드 검증 (강한 보안 X, 우발 노출 차단 용)
- `sessionStorage.setItem('nag-auth','1')` 세션 단위 기억
- 좌하단 🔒 버튼으로 즉시 재잠금

### 인터랙티브 요소
- 호버 효과: KPI 카드 떠오름, 패키지 카드 그림자 글로우
- KPI 숫자 카운터 애니메이션 (IntersectionObserver 트리거)
- 클릭 시 confetti burst (표지 타이틀 · 엠블럼 · s18)
- 표지 엠블럼 마우스 패럴랙스 (rotateY/X)

---

## 📅 변경 이력 (대화 흐름 + Git 커밋)

### Session 1 — 초기 생성 (2026-05-12)
1. 사용자: "salesdeck_asiangame 폴더 파일들로 2026 아시안컵 데크 만들기, 월드컵 PPTX 형식 참고, HTML로"
2. 처음엔 "AFC 아시안컵 사우디아라비아" 톤으로 만듦 (빨강+네이비 18 슬라이드)
3. 사용자 정정: "2026 아이치-나고야 아시안게임 (Asian Games)이지 Asian Cup 아님"
4. 컬러 팔레트 변경: 사용자가 제공한 `aichi-nagoya2026.org` 사이트의 CSS에서 컬러 직접 추출
5. 항저우 PDF + 위키 (사내) 데이터 반영: 1.77억 QC, 신유빈 191만, 페이커 46만 등 PDF 직접 인용

### Session 2 — OCA 엠블럼 + 인터랙티브
6. 사용자가 OCA(Olympic Council of Asia) 태양 엠블럼 이미지 제공 → SVG로 재현 (욱일기 아님 명확화: 16개 광선이 뾰족+물결 화염 교차)
7. Aichi-Nagoya 2026 공식 엠블럼 이미지 제공 → 3개 초승달 SVG로 재현
8. 카운터 애니메이션 / 호버 효과 / confetti 추가
9. 폰트 나눔스퀘어 네오 시도 (CDN URL 시행착오 끝에 fonts-archive로 확정)

### Session 3 — 디테일 다듬기 (수십개 항목)
10. 슬라이드 잘림 fix (s13 5-tier 카드, s14 GOLD 패널)
11. 슬라이드 순서 재배치: 패키지 구성 → APPENDIX 상품 소개 (Chapter 1 → Appendix)
12. 5p 한국 대표팀 일정을 9개 종목으로 대폭 확장 (양궁·사격·펜싱·태권도·e스포츠·야구 등)
13. 4p 큰 박스 뱃지(45/⭐/⏰/▲) 제거 — AI 느낌 정리
14. 빨간 라인 eyebrow 전역 숨김 (`.eyebrow{display:none}`)
15. 표지: 위키 로고 → 이미지 placeholder (사용자가 직접 추가)
16. NAVER 로고: 초록 = Wikipedia Commons / 흰색 = freebiesupply + filter
17. 마지막 페이지 월드컵 데크 포맷으로: 빨강 배경 + NAVER + 아이치 로고 + "E.O.D." + 문의 DL

### Session 4 — GitHub Pages 배포 (2026-05-13)
18. `git init`, `.gitignore`, `README.md`, `index.html` (copy of main HTML), `images/.gitkeep`
19. naversalesplanning/asiangame2026 리포 푸시 권한 부족 (403) → 사용자가 다른 GitHub 계정으로 `gh auth login` 후 재시도 성공
20. GitHub Pages 활성화 (main 브랜치 root, HTTPS enforced)
21. PPTX vs GitHub Pages 비교표 작성 → HTML 메일로 본인 발송 (`nworks mail send`)

### Session 5 — 발표 모드 + 인쇄 최종 다듬기
22. 프리젠테이션 모드 센터링 버그 (translate-50% 이슈) → flex 센터링으로 fix
23. PDF 자동 가로 인쇄: `@page{size:297mm 210mm;margin:0}` + `print-color-adjust:exact`
24. 프리젠테이션 viewport 채움 시도 → 챕터 디바이더 등 깨짐 → 16:9 strict 복귀 (디자인 무결성 우선)

### Session 6 — 수정모드 + 원클릭 PDF 다운로드 (2026-06-08, 현재)
25. **수정모드 추가**: 좌하단 툴바 `✏️ 수정` 버튼 + 단축키 `E` (게이트 해제 후 노출, 프리젠테이션 중 숨김)
    - `body.editing` 토글 + 상단 노란 안내 배너
    - 텍스트 편집: 문서 순서 기반 말단 텍스트 요소(자식요소 없음 또는 `<br>`만)에 `data-eid` 부여 → `contenteditable`. SVG/placeholder/버튼/입력 제외. 502개 요소 편집 가능
    - 이미지 편집: `img.mock-img / .aichi-logo / .aichi-img` 부모를 `.img-editable` 핫스팟화 → 클릭 시 파일선택 → 교체. 14개 이미지
26. **브라우저 저장**: 텍스트 → `localStorage["nag-edit-text-v1"]` (input 디바운스 400ms), 이미지 → **IndexedDB**(`nag-edits`/`img`, 용량 한계 회피). `↺ 초기화` 버튼으로 전체 원복(reload)
    - ⚠️ 이 브라우저에만 저장 — GitHub Pages 배포본/타 기기 미반영 (사용자 선택)
    - 텍스트 복원은 카운터 애니메이션 init보다 먼저 실행 → 수정한 숫자도 해당 값으로 카운트업
27. **원클릭 PDF 다운로드**: 기존 인쇄(`window.print()`) 버튼 제거 → `⬇ PDF 다운로드`로 교체
    - `html2canvas`+`jsPDF` CDN **지연 로드**, 18장 각 1600×900 렌더 → A4 가로 PDF(16:9 레터박스) → `2026_AsianGames_AichiNagoya_NaverPremium.pdf`
    - 진행률 라벨("PDF 생성 중 5/18…"), 실패 시 `Cmd/Ctrl+P → PDF로 저장` 폴백 안내
    - ⚠️ CORS: 외부 CDN 이미지가 차단되면 PDF에서 빈칸 가능
28. 편집 중 방향키가 슬라이드 이동으로 새지 않도록 기존 키보드 핸들러에 `isContentEditable` 가드 추가, confetti 핸들러에 `!editing` 가드 추가
29. 설계 문서: `docs/superpowers/specs/2026-06-08-edit-mode-and-pdf-design.md`
30. 헤드리스 Chrome 검증: 런타임 에러 0 / 텍스트 502·이미지 14 인식 / 수정토글·localStorage 저장·E키 토글 정상

### Session 6b — 수정모드 시크릿화 + 배포용 HTML 내보내기 (2026-06-08)
31. **시크릿 진입**: 수정/내보내기/초기화 버튼을 평소엔 숨김(`#editBtn,#exportBtn,#resetBtn{display:none}`).
    URL에 `?edit=nag-edit`(또는 `#nag-edit`)가 있을 때만 `body.edit-enabled` 부여 → 버튼 노출 + `E`키 단축키 활성화. (`const EDIT_KEY='nag-edit'`)
    - 보통 사용자/광고주는 버튼 자체를 못 봄. 편집 권한자만 URL로 진입.
32. **배포용 HTML 내보내기** (`💾 배포용 저장`, 수정모드일 때만 노출):
    - 현재 DOM을 복제 → `contenteditable`/`editing`/`presenting`/`edit-enabled` 제거, 숨김 파일입력·지연로드 라이브러리 스크립트 제거 → `<!doctype>` 붙여 `index.html`로 다운로드
    - 텍스트 편집 + 교체 이미지(data URL)가 **파일 안에 그대로 구워짐** → 이 파일을 git에 push하면 모두가 편집본을 봄
    - ⚠️ 중요: 브라우저 저장(localStorage/IndexedDB)은 파일에 안 담김. **배포 반영하려면 반드시 `💾 배포용 저장`으로 받은 index.html을 push**해야 함
33. 헤드리스 Chrome 검증: URL 키 없으면 버튼 숨김(display:none) / `?edit=nag-edit` 시 노출 / 내보낸 HTML에 편집 텍스트·이미지 bake 확인 / body 클래스·contenteditable 속성 제거 확인

### Session 7 — 콘텐츠 암호화 + AM 슬라이드 빌더 (2026-06-10)
34. **콘텐츠 암호화 (StatiCrypt 방식)**: `.deck`(18장)을 **AES-256-GCM ciphertext**로만 소스에 둠. 소스 보기 해도 단가/내용은 암호문(`/*ENC-START*/const ENC_SALT/ENC_IV/ENC_DATA/*ENC-END*/`)만 보임.
    - 게이트 비번 `nasiangame2026`이 곧 **복호화 키**: PBKDF2(SHA-256, 250k iters) → AES-GCM-256. 비번 입력 → 복호화 → `.deck` 주입 → `initDeck()`. 비번은 `sessionStorage['nag-pw']` 캐시(같은 탭 자동 해제), 🔒=캐시 삭제+reload.
    - 오답 비번은 GCM 인증 실패로 거부(별도 해시 불필요). 평문 백업은 `_plaintext_backup_index.html`(gitignore). 최초/재빌드: `tools/encrypt.mjs`(Node WebCrypto, 동일 파라미터).
35. **git 히스토리 평문 제거**: 첫 커밋부터 평문이라 전 히스토리를 단일 클린 커밋으로 squash(`56ea771`) 후 force-push. 백업 번들 `Documents/asiangame_history_backup_01e5d03.bundle`. (GitHub stale 커밋은 SHA로 한동안 잔존 — 필요 시 Support GC.)
36. **💾 저장 시 새 비밀번호**: `prompt()`로 "새 비밀번호(빈칸=기존 유지, 취소=중단)". 새 비번 입력 시 그 비번으로만 열리는 파일 → **광고주별 덱 분리**(예: 삼성용 별도 비번). 저장 알림에 최종 비번 표시.
37. **AM 모드 (`?edit=nag-am`, `AM_KEY='nag-am'`)**: `body.am-mode`. 표준 18장 **하드락**(수정·삭제·이미지교체 불가, 🔒 "표준 장표 — 수정 불가" 배지). `nag-edit`(작성자)는 전체 편집(회귀 없음). 잠금 판정 `isLocked()`.
38. **슬라이드 추가/삭제 (커스텀 장표만)**: `➕ 슬라이드 추가` 팔레트 템플릿 3종 — **스페셜오퍼**(`tpl-offer`) / **빈배경**(`tpl-blank`, 이미지 1) / **패키지 세트**(`tpl-pkg-detail`+`tpl-pkg-price` 2장 동시, GOLD 상세 s14 + 단가표 s15 복제, **단가는 ○억·— 플레이스홀더**라 평문 미노출). 추가 장표(`data-custom`)만 편집·🗑삭제·↕이동. 작업 중 `nag-custom-v1` localStorage 스크래치(`data-scratch`) 보존, 💾 시 ciphertext에 baked+스크래치 정리.
39. **삽입 위치 선택**: 수정모드에서 장표 사이 `＋ 슬라이드 추가하기` 존(hover) 클릭 → 그 자리에 삽입. 툴바 ➕는 맨 뒤 기본. 존은 edit-only, export 시 제거.
40. **단가표 인라인 편집**: 커스텀 단가표(`.tbl`)에 `＋ 행 추가` + 행별 `✕` 삭제 + **TOTAL(단가/노출수) 자동 합산**(판매가는 수동). 컨트롤(`.slide-ctrls/.lock-badge/.insert-zone/.rowdel/.addrow-btn`)은 export 시 모두 제거.
41. (보류) 엑셀/CSV 임포트 — 라이브러리 의존·열매핑 비용으로 후속. 인라인 행 편집으로 대체.
42. **헤드리스 CDP 종합검증(라이브 URL, 18항목 통과)**: 복호화·18장 / AM 표준잠금·배지 / 작성자 회귀없음 / 삽입존·위치정확 / 패키지세트 +2·실단가없음 / 행 추가·삭제·TOTAL 자동합산(300,000,000) / 오퍼추가·커스텀삭제 / 새비번 재암호화→새비번만 복호화·기존거부.

> ⚠️ 미결: 패키지 세트 템플릿에 상품 구성 항목명(트리플크라운 등)은 평문 유지 중(단가만 비움) — 항목명까지 비울지 미정. AM 배포 가이드 문서는 "수정 완료 후" 작성 예정.

### Session 8 — 티어별 상세 슬라이드 4장 (2026-07-06)
43. **패키지마다 "상세(상품 구성) + 단가표" 2장 세트로 통일**: GOLD만 상세(s14)+단가표(s15) 세트였고 나머지 4티어는 단가표만 있던 것을 수정. SILVER/BRONZE/FINALIST/OPENER 각 단가표 앞에 s14 스타일 상세 슬라이드 삽입(`id=s14-silver/-bronze/-finalist/-opener`, `class="slide s14 pk-*"`). 총 22→**26장**.
    - 구성 카드(cats)는 각 단가표의 영역/지면 행을 그대로 인용(임의 추가 없음). 3영역 티어는 `style="grid-template-columns:repeat(3,1fr)"`.
    - 목업 이미지 placeholder: `images/slide14-<tier>-pc.png` / `slide14-<tier>-phone.png` (8개, 직접 추가 필요)
44. **fix: `.pk-* .name` 그라데이션 텍스트 버그** — `background:...!important` 쇼트핸드가 `background-clip:text`를 border-box로 리셋해 티어명이 그라데이션 바(bar)로 뭉개짐(기존 배포 단가표 4장도 동일 증상). → `background-image:...!important` + `background-clip:text!important`로 교정.
45. PDF 내보내기 `solidFill`에 티어별 단색 추가(실버 #a9a9a9 / 브론즈 #b87333 / 퍼플 #6b6fae / 틸 #2fa8a3) — 기존엔 s14/s15 name이 전부 금색으로 강제됐음.
46. 검증: 복호화 라운드트립 일치 / 오답 거부 / 단가 평문 누출 0(금액 패턴 히트는 전부 rgba 색상값) / 26장 렌더·순서 정확 / 신규 8장 1600×900 overflow 0 / 4장 스크린샷 시각 확인. 커밋 `fef590b` push 완료.
47. 상세 페이지(s14) 좌측 패널 폭 36%→32% — 단가표(s15)와 일치시켜 세트 연속성 확보 (`93376c4`).

### Session 8b — 패키지 라인업 전면 교체: 정본 시트 변경 (2026-07-06)
48. **⚠️ 단가 정본 시트 변경**: `부킹용(최종)` 시트(GOLD 10억~OPENER 1억 5종)가 아니라 **`2026 아시안게임` 시트의 공통패키지**가 정본으로 확정(효주님 확인). 라인업 = **5억/3억/1억/VIDEO/클립** 5종.
49. **패키지 전면 재구성** (네이밍: 금액 3티어는 메달 유지 + 특화 2종 영문, 효주님 선택):
    | 패키지 | 구성(구좌) | value | 서비스율 | 판매가 | 판매 한도 |
    |---|---|---|---|---|---|
    | GOLD(구 5억) | 트리플크라운1·PC전면형1·프리롤/미드롤3·치지직FV1·통검1·치지직 메인브랜딩1 | 590M | 15.3% | 5억 | 3구좌 |
    | SILVER(구 3억) | 스포츠피드1st 6·PC전면형1·프리롤/미드롤2·통검1 | 340M | 11.8% | 3억 | 8구좌 |
    | BRONZE(구 1억) | 스포츠피드1st 6·프리롤/미드롤1 | 110M | 9.1% | 1억 | 15구좌 |
    | VIDEO | 프리롤/미드롤1 | 50M | 0%(정가) | 5천만 | — |
    | CLIP | 클립(1초 범퍼)1·숏폼 1st 1 | 150M | 33.3% | 1억 | 3구좌 |
50. s13 그리드 + 상세/단가표 10장 전부 재생성(총 26장 유지). id: `s14`/`s15`(GOLD), `s14-silver`~`s15-clip`. FINALIST/OPENER 폐기 → CSS `.pk-finalist/.pk-opener` → `.pk-video`(레드)/`.pk-clip`(퍼플)로 개명 — s13 그리드 4·5번 카드 색과 일치. 이미지 placeholder: `slide14-video/-clip-{pc,phone}.png`.
51. 검증: 라운드트립/평문누출0/26장/overflow 0/TOTAL·판매가 5종 모두 엑셀 일치/스크린샷 4장 확인.
52. 여백 정리(폰트/행높이 확대, `08de3d2`) → 좁은 창 잘림 발견 → s13/14/15 **px→cqw 전환**(`e11b497`) → 사파리 등에서 여전히 잘림 → **overflow-proof 구조**(`8a4de19`): `.devices{min-height:0;overflow:hidden}` + 카드 `flex-shrink:0` — 공간 부족 시 목업만 축소, 구성 카드는 절대 안 밀림. 폰트 25% 스트레스 테스트 통과.
53. **1차 annotation 배치 반영** (`9170737`): 효주님이 📌 수정요청 모드로 보낸 14건 중 13건 반영(s3 한줄, s4 카드 위치, s5 타임라인 선 정렬, s6 숫자 확대, s13 박스 균일화+헤드 확대, s14 헤드라인·좌패널 확대, s15 서비스/판매가 단가열 정렬, s17 제목, s18 중앙정렬, s1 커버 엠블럼 삽입+placeholder 숨김). 미반영 1건: `#cs-17` 커스텀 장표 삭제 — 브라우저 localStorage에만 존재해 수정모드 🗑로 본인 삭제 필요. ⚠️ Pages deploy가 "Deployment failed, try again later"로 간헐 실패 — `gh api -X POST .../pages/builds`로 강제 리빌드하면 해결.
54. **📌 수정요청(annotation) 모드** (2026-07-06): `?edit=nag-edit` 툴바에 `📌 수정요청` 버튼. 켜면 장표 아무 요소나 클릭 → 메모 입력 → 번호 핀 표시. 우하단 패널에서 `📋 요청 복사` → 슬라이드 id·CSS 경로·eid·현재 텍스트·메모가 포함된 목록이 클립보드로 → Claude에게 붙여넣으면 정확한 위치 수정 가능. `nag-annot-v1` localStorage 저장(브라우저 단위), 핀/패널은 export·PDF에서 제거, 일반 URL에선 버튼 숨김. 수정모드와 상호배타(요청모드 켜면 편집 꺼짐).

### Session 9 — 패키지 라인업 전면 개편 + 외부판매 공지 (2026-07-13)
55. **⚠️ 정본 시트 또 변경**: `2026 스포츠 세일즈패키지 _ 상품&세일즈 (1).xlsx`의 `2026 아시안게임` 시트 재확인 결과 라인업이 바뀜. 기존 GOLD 5억/SILVER 3억/BRONZE 1억/VIDEO/CLIP → **GOLD 3억 / SILVER 2억 / BRONZE 1억 / OPENER 3천만** 공통 4티어 + **종목 특화(축구·야구 각 3억)**. 브랜딩 2억(구좌 0)은 미판매 제외.
    | 티어 | 판매가 | value | 서비스율 | 구좌한도 | 구성 |
    |---|---|---|---|---|---|
    | GOLD | 3억 | 380M | 21.1% | 2구좌 | 트리플크라운1·PC전면1·프리롤/미드롤3·치지직FV1·통검1·특집배너3종1 |
    | SILVER | 2억 | 240M | 16.7% | 3구좌 | PC전면1·풀스채2·스포츠피드1st 4·프리롤2·통검1 |
    | BRONZE | 1억 | 110M | 9.1% | 5구좌 | 풀스채2·스포츠피드1st 4·프리롤1 |
    | OPENER | 3천만 | 30M | 정가 | 1구좌 | 프리롤/미드롤1 |
56. **덱 26→24장**: s13 그리드 5카드→**4카드**(CSS `.s13 .pks` repeat(5,1fr)→repeat(4,1fr) — 유일한 index.html CSS 수정), GOLD/SILVER/BRONZE 상세+단가표 재작성, VIDEO세트→**OPENER**로 개명(id `s14-opener`/`s15-opener`, 클래스 `pk-video`(레드) 재사용), **CLIP 세트 2장 삭제**.
57. **s16 종목 단독 = 효주님 제공 원본 이미지 형태로 확정**: 6종(축구/야구/LoL/양궁/탁구/배드민턴)이던 걸 **축구·야구 2카드**로 축소(농구&배구 포함 나머지 제외). 카드 내용은 원본 슬라이드 이미지대로 3항목 — 스페셜 템플릿(MO) 5,000만 노출 / 브랜드 트렌드 스토리 홈 단독 / PC 사이드스킨·MO 띠배너 — + **1구좌 단독 2.5억원**. (트리플크라운 단독+결승우선권/3억 버전은 폐기.) 2카드 중앙 정렬 2열(`repeat(2,minmax(0,34cqw));justify-content:center`), 카드 풀높이 채움.
58. **검증**(CLI+헤드리스): 복호화 라운드트립 일치 / 오답 거부 / 평문 금액 누출 0(색상값만) / 24장 / 신규·변경 패키지 10장 전부 1600×900 overflow 0 / s13·s16·s15(GOLD) 스크린샷 시각 확인 / GOLD TOTAL 380M·판매가 300M 표 일치.
59. **외부판매 공지 초안**: EWC 생중계 패키지 공지 포맷 참고. 핵심 = 세일즈덱은 신청자에게만 개별 공유(공지에 링크 미노출) + 네이버폼 `naver.me/F6Qiewri` 선착순 접수. (대회일정·수수료율 등 「」 확정 대기.)
61. **상품 소개(Appendix) 상품 8종 추가 (효주님 요청, 월드컵 PPTX 포맷 참고, 덱 24→32장)**: 아시안게임 패키지 포함 상품을 상품당 1장으로 추가. s12 디바이더 뒤 → 신규 8장 → 기존 s9/s10/s11 순. **최종 포맷 = `.s-cat`(월드컵 Appendix 스타일)**: 좌측 다크 사이드바(브랜드 + 빨간 카테고리 헤더 + 카테고리 내 상품 리스트, 현재 상품 강조 `pi.on` + 전체 패키지 확인 버튼) / 우측 크림 영역(헤드라인 + 설명 + 목업). 카테고리 분류(효주님 지정): **메인**(트리플크라운 MO·PC전면형·통합검색 상단/중단·스포츠피드1st) / **디스플레이**(풀스크린채널) / **치지직**(치지직 프리미엄 FirstView) / **특집페이지**(특집배너3종) / **동영상**(프리롤·미드롤). id `p-triple/pcfront/search/sportsfeed/fullscreen/chzzk/special-banner/video`. 목업: `.pmock.mo`(폰) / `.pmock.pc`(PC전면형만 가로). 목업 placeholder `images/prod-*.png`. ⚠️ 함정: `.slide` 기본 배경이 `--ink`(다크)라 `.s-cat`(단일클래스)로는 `.deck .slide`(0,2,0)를 못 이겨 main이 다크로 떠 검정 헤드라인이 안 보였음 → `.s-cat .main{background:var(--cream)}` + `.slide.s-cat`로 특정도 상향해 해결. 검증: 32장·8장 overflow 0·main 크림배경·헤드라인/설명 가독·평문단가 누출 0·자동해제 유지.
62. **상품 소개 실제 목업 이미지 삽입 (월드컵 PPTX에서 추출)**: 월드컵 PPTX 상품 슬라이드(21~30)의 실제 노출 예시 스크린샷(예시 브랜드=네이버배송·미션임파서블·라인프렌즈·네이버페이·KBS 등, FIFA/월드컵 문구 없음)을 python-pptx로 추출→Pillow로 max 900px 리사이즈→`images/prod-*.png`로 저장. 매핑: triple←s23, fullscreen←s24, sportsfeed←s25, video←s26, chzzk←s27(폰), special-banner←s30, search←s22(가로). **search는 이미지가 가로형이라 슬라이드를 `pmock pc`로 변경**. **트리플크라운은 두 화면(`.stage.twin2`)** — 왼쪽 `prod-triple-main.png`(메인 상단 노출, 슬23 MEDIA 포스터 프레임 추출) + → 화살표 + 오른쪽 `prod-triple-full.png`(확장 시 전면, s23p0), 캡션 포함. 덱은 이미 `images/prod-*.png` 경로 참조라 이미지 파일만 넣으면 자동 표시(재암호화 불필요, search 컨테이너 변경만 재빌드). **PC전면형(prod-pcfront)**은 PPTX상 벡터+영상이라 추출 불가였으나, **효주님이 네이버 PC 홈(헤드라인DA·타임보드·롤링보드·좌우스킨 지면 표시) 예시 이미지를 직접 제공**해 `images/prod-pcfront.png`로 반영 → **8/8 실이미지 완료**. 검증: 8장 이미지 로드·스크린샷(트리플크라운·통합검색·PC전면형) 확인.
63. **상품 소개 목업/사이드바 UI 재디자인 (효주님 피드백: 확대 이미지 이상, 사이드바 안 예쁨)**: ⓐ 목업을 고정비율 `.pmock`+`object-fit:cover`(크롭→과확대) → **`.shot`(원본 비율, `max-height:100%`/`max-width:90%`, 크롭 없음) + 둥근모서리+그림자로 띄우는 방식**으로 교체(세로 긴 스포츠피드 등 과확대 해결). placeholder도 `.ph-box` 둥근 박스로 통일(onerror 시 노출). pc/mo 컨테이너 구분 폐지(원본 비율이라 불필요). ⓑ 사이드바 상품 리스트를 **둥근 모서리 카드**(`pi` border-radius:14px+미묘한 bg/border, `pi.on`=빨강 그라데이션 tint+빨강 border)로, `plist`는 빨간 띠 바로 아래 상단 정렬(`margin-top`), `allbtn`은 `margin-top:auto`로 하단 고정. cat-head(빨간 띠)는 유지. (※ 처음엔 plist를 세로 중앙정렬했으나 단일상품이 가운데 떠 허전하다는 피드백으로 상단정렬로 롤백.) 검증: 8장 원본비율 표시·overflow 0·단일/다중 카테고리 균형.
60. **입장 시 비번 프롬프트 제거 — 자동 열림 (효주님 요청, 최종)**: 시행착오 정리 — ⓐ "입장 비번 제거"를 평문 OPEN(암호화 해제)으로 잘못 처리 → ⓑ "암호화 말고 입장 비번만" → 내장 키 자동해제로 수정 → ⓒ "페이지에서 지우고 메모로만"을 게이트 원복으로 오해 → ⓓ "비번 없애달랬잖아" → **최종: 무프롬프트 자동해제**. 현재 index.html: 게이트 `hidden`, 부트 IIFE `(function(){ unlockWith('nasiangame2026'); })();`(내장 키 자동 복호화), `#lockBtn` 숨김. **덱은 소스에 암호문(ENC) 유지 → 평문 단가 미노출**. 검증: sessionStorage 비운 신규 방문자도 프롬프트 없이 24장 자동 렌더. ⚠️ 트레이드오프: 자동해제라 복호화 키 `nasiangame2026`이 JS 소스에 들어감(작정하면 복호화 가능하나 단가가 평문으로 바로 보이진 않음). 비번은 `_password_memo.md`(gitignore) + 기억에도 보관. 재빌드 베이스는 `/tmp/final_enc.html`(표준 게이트 암호화본)에 이 3개 편집 적용.

64. **종목 특화 단가 엑셀 검수 → 3억/2구좌로 정정 (효주님 A안)**: 엑셀 `2026 아시안게임` 시트 판매가 재검수 결과 공통 4종(GOLD 3억/SILVER 2억/BRONZE 1억/OPENER 3천만)은 정확, 그러나 **종목(축구/야구)=판매가 3억·2구좌·GOLD 동일구성**임을 확인(시트엔 2.5억·스페셜템플릿 없음 — 덱의 2.5억은 월드컵 참고이미지 잔재). s16을 "종목 단독 2.5억/1구좌(스페셜템플릿 구성)" → **"종목 특화 3억/2구좌(트리플크라운·PC전면·프리롤3·치지직FV·통검·특집배너3종 = GOLD 구성)"**로 교체. 외부판매 공지도 동일 반영. 검증: s16 overflow 0·스크린샷 확인.

65. **유의사항(s17) 전면 교체 — 효주님 제공 19개 항목 문장 그대로**: 기존 8개 → **19개**(운영·부킹·NOSP·위약금·중간광고 라인 등). 20개 못 들어가 s17 CSS 컴팩트화(폰트 .74cqw, 패딩/갭 축소, 2단 grid align-content:start). 1장에 overflow 0으로 수용. 수수료율 15% 포함.

### Session 10 — s16 문구 통일 + UTM 배포 링크 기록 (2026-07-16)
66. **s16 종목 특화 좌측 pitch 문구 통일**: 좌측 pitch `축구, 야구 종목 조별리그 일정(대한민국 경기 시간)에 GOLD 패키지 구성을 집행하는 패키지입니다.` → 우측 lead와 동일한 `축구, 야구 종목 조별리그 일정에 GOLD 구성을 집행할 수 있는 패키지입니다.`로 교체(라운드트립 검증·재암호화·push·Pages 배포 반영 확인). 커밋 `40fb10f`.
67. **⚠️ 배포용 UTM 링크 2개 = 정본 기록**(그동안 미기록이라 분실 위험이었음): GA4 `G-E5DR61KNGK`. **① 내부(AM 공지/영업 메일링)** `?utm_source=am&utm_medium=internal&utm_campaign=asiangames2026` / **② 외부(NOSP 공지)** `?utm_source=nosp&utm_medium=notice&utm_campaign=asiangames2026` (베이스 URL = 배포 주소). 덱 GA 제외 로직 `/(nag-edit|nag-am)/i`는 두 링크에 오작동 안 함(검증 — `am`은 `nag-am`과 매칭 안 됨). GA4 구분: `획득 > 트래픽 획득`에서 **세션 소스**(am/nosp) 또는 **세션 매체**(internal/notice)로. campaign은 동일하니 소스/매체로 갈라야 함. `utm_medium=internal`은 기본 채널그룹 미인식이라 명시적 소스/매체 측정기준 사용. 표준보고서 24~48h 지연(즉시확인=실시간/DebugView). 내부망·애드블록으로 내부(am) 과소집계 가능.

---

## 📊 Git 커밋 히스토리

| Commit | 메시지 | 날짜 |
|---|---|---|
| `1ad4ab4` | Initial deploy: 2026 Aichi-Nagoya Asian Games sales deck | 2026-05-13 |
| `442364f` | Fix: presentation centering + auto landscape PDF | 2026-05-13 |
| `a50734b` | Presentation full-viewport fill + A4 landscape color print | 2026-05-13 |
| `c89a521` | Restore 16:9 strict in presentation mode | 2026-05-13 |
| `56ea771` | **(히스토리 재작성)** 단일 클린 스냅샷 — 과거 평문 단가 제거 + 암호화 발행본 | 2026-06-10 |
| `e696063` | feat: 새 비밀번호 저장 + AM 슬라이드 빌더(추가/삭제) | 2026-06-10 |
| `f5208a8` | feat: '패키지 세트' 팔레트 템플릿(GOLD 2장, 단가 플레이스홀더) | 2026-06-10 |
| `ff7c14e` | feat: 장표 사이 '＋' 삽입 위치 선택 | 2026-06-10 |
| `0b593f0` | feat: 단가표 인라인 행 추가/삭제 + TOTAL 자동합산 | 2026-06-10 |
| `9e67a61` | tweak: 삽입 라벨 → '슬라이드 추가하기' | 2026-06-10 |

---

## 🔑 운영 가이드

### 비밀번호 (= 복호화 키, Session 7부터)
- `nasiangame2026` — 게이트 비번이 곧 AES 복호화 키. 한 번 입력하면 `sessionStorage`에 캐시.
- **비번 변경**: 소스 직접 수정 불가(덱은 암호문). `?edit=nag-edit`로 접속 → `💾 배포용 저장` 시 "새 비밀번호" 입력 → 그 비번으로 재암호화된 index.html을 push. (또는 `node tools/encrypt.mjs <새비번>`로 평문 백업 재암호화.)
- 편집 진입: `?edit=nag-edit`(작성자 전체편집) / `?edit=nag-am`(AM — 표준 잠금, 커스텀 장표만)

### 이미지 추가
- `images/` 폴더에 위 슬라이드 구성표의 파일명대로 PNG 저장 후 git push
- 이미지 없으면 점선 placeholder가 자동 표시되며 파일 경로 안내

### 발표 시 단축키
- F → 프리젠테이션 시작
- ESC → 종료
- ←/→/Space/PageUp/PageDown → 슬라이드 이동
- Home/End → 처음/끝
- 좌하단 PDF 버튼 → A4 가로 컬러 인쇄/저장

### 모니터 비율
- 16:9 (1920×1080, 2560×1440, 외부 모니터/프로젝터 대부분): 화면 꽉 참
- 16:10 (MacBook 1440×900 등): 상하에 얇은 letterbox
- 4:3 (구형 프로젝터): 상하에 큰 letterbox

---

## ⚠️ 알려진 트레이드오프 / 향후 보완 가능

1. **letterbox** — 16:9 외 모니터에서는 검은 여백 발생 (디자인 무결성 우선 선택). 향후 동적 비율 감지로 보완 가능.
2. **비개발자 수정 접근성** — 텍스트 수정에도 HTML 편집 필요. 슬라이드 데이터를 별도 JSON으로 빼면 비개발자도 수정 가능.
3. **광고주 신뢰성** — 도메인이 `*.github.io`라 광고주 인식 거부감 가능. CNAME으로 `*.navercorp.com` 서브도메인 연결 검토.
4. **이미지 16개** — 모두 placeholder 상태. 실제 노출 화면 캡처/디자인 시안 필요.
5. **PPTX 자동 변환** — GitHub Action으로 HTML→PPTX 파이프라인 구축 시 광고주 메일 첨부도 자동화 가능.

---

## 📧 본인에게 발송한 내부 메일

- **일시**: 2026-05-13
- **대상**: hyoju.cheong@navercorp.com (본인)
- **제목**: `[배포] 2026 아이치-나고야 아시안게임 세일즈덱 — GitHub Pages 시범 운영 안내`
- **내용**: 배포 URL · 사용법 · PPTX vs GitHub Pages 비교표 (11항목) · 하이브리드 운영안 (4 시나리오) · 보완 검토 사항 (4건)

---

## 🔗 참고 링크

- 배포: https://naversalesplanning.github.io/asiangame2026/
- 리포: https://github.com/naversalesplanning/asiangame2026
- Wikipedia 공식 엠블럼: https://upload.wikimedia.org/wikipedia/en/thumb/4/4d/2026_Asian_Games_logo.svg/250px-2026_Asian_Games_logo.svg.png
- 아이치-나고야 2026 공식: https://www.aichi-nagoya2026.org/en/
- 폰트 CDN: https://cdn.jsdelivr.net/gh/fonts-archive/NanumSquareNeo/NanumSquareNeo.css
- NAVER 로고 CDN: https://upload.wikimedia.org/wikipedia/commons/thumb/2/23/Naver_Logotype.svg/3840px-Naver_Logotype.svg.png

---

## 🏷 라이선스 / 권리

- NAVER Corp. — 광고 패키지 / 데이터 / NAVER 로고
- 2026 Asian Games Aichi-Nagoya OCAA — 대회 정보 / 공식 엠블럼
- 본 자료는 사내 영업 및 광고주 제안 목적이며, 외부 공유 시 사전 협의 필요
