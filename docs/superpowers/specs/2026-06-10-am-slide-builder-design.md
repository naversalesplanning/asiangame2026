# AM 슬라이드 추가/삭제 (라이트 커스터마이징 + 하드락) · 설계

> 작성: 2026-06-10
> 목표: 다른 AM이 표준 덱을 건드리지 않고 광고주별 맞춤 장표(스페셜 오퍼 등)를 추가/삭제.

## 확정 결정 (사용자)
- 범위: **라이트 커스터마이징** (표준 덱 유지 + 장 추가/삭제 정도)
- 핵심 장표 보호: **하드락** (표준 장표 수정·삭제 불가)

## 권한 모드 (편집 진입 키 2종)
- `?edit=nag-edit` → **작성자 풀편집** (기존 그대로): 전체 수정 + 어떤 장이든 추가/삭제
- `?edit=nag-am` → **AM 모드 (신규)**: `body.am-mode`. 표준 장표 **완전 잠금**.
  AM은 *자기가 추가한 `[data-custom]` 장표만* 편집/삭제/이동 가능.
- 둘 다 `body.edit-enabled` 부여. `AM_KEY='nag-am'`.

## 슬라이드 추가 팔레트
- 수정모드 툴바에 `➕ 슬라이드 추가` 버튼 → 팔레트(모달) 표시.
- 템플릿 = 파일 내 숨김 `<template>` (외부 의존성 0, 기존 CSS 재사용):
  - `tpl-offer` — **스페셜 오퍼 포유**: 다크 히어로(`.s-offer`), eyebrow "SPECIAL OFFER",
    H1 "Special Offer <em>for You</em>", 편집 가능한 서브카피 + 오퍼 카드 2~3개(제목/설명/혜택) + 광고주 로고 placeholder.
  - `tpl-blank` — **빈 배경**(`.s-blank`): `--ink` 배경 + topbar + 편집 가능한 H2 1개 + 본문 1개. 자유 캔버스.
- 삽입: 템플릿 clone → `data-custom="1"` 부여 → 덱 끝에 append → `enhanceCustomSlide()` →
  텍스트 eid/리스너 + 이미지 핫스팟 + 컨트롤 부착 → HUD 갱신 → (편집 중이면) contenteditable on.

## 커스텀 장표 컨트롤 (편집모드, `[data-custom]`만)
- `.slide-ctrls` 주입: **🗑 삭제 · ↑ 위로 · ↓ 아래로**.
- 삭제 → confirm → remove + HUD 갱신 + 저장.
- 이동 → 인접 `.slide`와 swap + HUD 갱신 + 저장.

## 표준 장표 잠금 (AM 모드)
- AM 모드 + 편집 시 표준 장표(`:not([data-custom])`)에 `.lock-badge`(🔒 "표준 장표 — 수정 불가") 주입.
- setEditing: AM 모드면 `[data-custom]` 안 요소에만 contenteditable. 이미지 핫스팟도 custom 한정.

## 저장 / 영속성
- 💾 export: 커스텀 장표는 `.deck` DOM에 있으므로 ciphertext에 **자동 포함**. (새 비번 기능과 연동.)
  - export 정리 시 `.slide-ctrls`/`.lock-badge`/`data-custom` 제거? → `data-custom`은 **유지**해야 재편집 때 인식.
    `.slide-ctrls`·`.lock-badge`·contenteditable·eid만 제거.
- 작업 중 새로고침 대비 localStorage `nag-custom-v1`:
  - add/delete/move/edit(디바운스) 시 커스텀 장표들의 `{idx, html}`(현재 outerHTML, 컨트롤/eid 제거본) 스냅샷 저장.
  - 복호화·주입 직후 복원: 저장된 순서/위치로 재삽입 → enhance.
- `↺ 초기화`: 텍스트맵·IndexedDB 이미지 + `nag-custom-v1` 모두 제거 후 reload.

## initDeck 통합
- 복호화로 deck 주입 후: 기존 텍스트/이미지 수집 → **커스텀 장표 복원** → enhance → 카운터 init.
- HUD 빌드/카운터 등 `.slide` 기준 로직은 복원 후 1회 실행 (순서 주의).

## 검증 (헤드리스 CDP)
- `?edit=nag-am`: 표준 장표 contenteditable 부재, custom만 편집 가능
- 팔레트로 offer/blank 추가 → `.slide` 수 +1, HUD +1, data-custom 표시
- 커스텀 장표 삭제 → 수 복귀
- 💾 재암호화본에 커스텀 장표 포함 + 복호화 왕복 일치
- 표준 장표 잠금(🔒) 표시 / 작성자 모드(nag-edit)는 전체 편집 유지(회귀 없음)

## 한계 / 비범위
- 드래그 정렬·다단 레이아웃 에디터는 비범위(라이트). ↑↓ 이동까지만.
- 컴포넌트 풀팔레트(KPI그리드/패키지표 등)는 후속 확장 — 본 v1은 offer/blank 2종.
