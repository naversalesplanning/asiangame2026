# 페이지 콘텐츠 암호화 (StatiCrypt 방식) · 설계

> 작성: 2026-06-10
> 목표: 라이브 소스에서 단가/금액이 안 보이도록 덱 내용을 AES-GCM ciphertext로 발행.
> 올바른 비밀번호 입력 시에만 브라우저에서 복호화되어 표시.

## 배경 / 문제

현재 `index.html`의 비밀번호 게이트는 **눈속임**이다:
- `const GATE_PW='nasiangame2026'` 가 소스에 평문 노출
- `.deck`(18장 슬라이드 + 단가표)이 평문 마크업으로 소스에 그대로 존재

→ "소스 보기" 한 번이면 비번도 가격도 전부 노출.

## 채택 결정 (사용자 확정)

1. **암호화 범위**: 덱 전체 (`.deck` 내부 마크업 전부)
2. **빌드 방식**: 브라우저 내장 (Web Crypto). 기존 💾 배포용 저장 버튼이 재암호화 담당. 일상 워크플로에 Node 빌드 단계 없음.
3. **비밀번호**: 게이트 비번 `nasiangame2026` 통합 (= 복호화 키). 세션 캐시 O.

## 암호 설계

- 키 유도: PBKDF2(pw, salt(16B random), 250,000 iters, SHA-256) → AES-256 키
- 암호화: AES-GCM(iv 12B random) over `deck.innerHTML` (UTF-8)
- 파일에는 base64 `salt`, `iv`, `ciphertext` 만 저장 — **비번/평문 가격 일절 없음**
- 비번 오류 → GCM 인증 태그 실패 → catch → "비밀번호가 일치하지 않습니다."
  (GCM 무결성 = 비번 검증. 별도 해시 불필요.)

## 단일 파일 구조 (발행본 = 편집본 동일 파일)

```
<body>
  <div class="gate"> … 비번 입력 폼 … </div>
  <div class="deck"></div>   ← 비어 있음 (복호화 시 주입)
  <toolbar/banner/...>
  <script>
    /*ENC-START*/const ENC_SALT="…",ENC_IV="…",ENC_DATA="…";/*ENC-END*/
    [crypto core: b64 helpers, deriveKey, decryptDeck, encryptDeck]
    [gate flow: submit→decrypt→inject→initDeck()→unlock, pw를 sessionStorage('nag-pw') 캐시]
    function initDeck(){ [기존 프리젠/HUD/카운터/confetti/parallax/편집·PDF IIFE 전부] }
  </script>
</body>
```

### 동작
- **뷰어**: 비번 입력 → 복호화 → `.deck`에 주입 → `initDeck()` → 발표/PDF (기존과 동일)
- **편집자**: `?edit=nag-edit` + 비번 → 복호화 → 라이브 DOM 편집 → 💾 → 현재 deck 재암호화 → 새 `index.html` 다운로드 → push
- **세션 캐시**: `sessionStorage['nag-pw']`. 같은 탭 새로고침 시 자동 복호화. 🔒 → 캐시 삭제 + reload (메모리의 평문 제거).

## 코드 변경

1. 기존 `GATE_PW` 평문 비교 게이트 → 암호 복호화 게이트로 교체.
2. deck 의존 init(프리젠/HUD/카운터/confetti/parallax/편집·PDF)을 `initDeck()` 안으로 이동, 복호화 후 1회 호출.
3. `exportHTML()` 재작성:
   - 편집 끈 뒤 deck clone에서 contenteditable/data-eid/data-ieid/img-editable/active 제거
   - `encryptDeck(pw, deckHTML)` → 새 salt/iv/data
   - documentElement clone에서 **`.deck` 비우고**, `/*ENC-START*/…/*ENC-END*/` 블록을 새 값으로 치환, 편집 클래스/파일입력/지연라이브러리 제거
   - `index.html` 다운로드 (평문은 출력에 절대 미포함)

## 최초 빌드 (부트스트랩)

`tools/encrypt.mjs` (Node webcrypto, 동일 파라미터):
1. 평문 작업본 `index.html` 읽기
2. `.deck` innerHTML 추출 → 암호화
3. deck 비우고 ENC 블록 채운 발행본으로 덮어쓰기

→ 저장소에는 **암호화본만** 남는다 (평문 작업본 미커밋).
이후 재편집은 브라우저 💾 가 담당하므로 평문 소스 파일 불필요.

## 검증

- Node 라운드트립 (encrypt→decrypt = 원본)
- Chrome `--headless --dump-dom`: 자동 복호화 사본 로드 → 18장 슬라이드/단가표 텍스트 존재 확인
- 발행본 raw HTML 에 "판매가"/단가 숫자 **부재** 확인

## 알려진 한계 (사용자 인지)

- 복호화 후 해당 뷰어 화면엔 보임 → PDF 저장 가능. "허들 상향"이지 완벽 아님.
- `nasiangame2026` 은 짧아 오프라인 무차별 대입 가능. 250k PBKDF2로 비용 상향. (사용자: 비번 유지 선택)
- **git 히스토리**의 과거 평문 커밋은 그대로 남음 (본 작업 범위 밖, 필요 시 히스토리 재작성 별도).
