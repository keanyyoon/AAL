# Glim — 이어받기(Handover) 브리프

> 이 문서 하나만 먼저 읽으면 현재까지의 맥락을 이어받아 작업을 계속할 수 있습니다.
> (폴더는 이미 링크됨 → 아래 파일들에 직접 접근 가능)

## 1. 제품 한 줄 정의
**Glim** — 11~15세 글로벌 학생용 **소크라틱 문해력 AI 튜터**. 답을 주지 않고 발문으로 스스로 사고하게 함. 문해력(의미·논리·지식)·상상력·서사력 육성 + 게이미피케이션. Web(태블릿·PC 우선), 영어 소재로 시작.

## 2. 세계관 & 디자인 언어 (반드시 유지)
- 세계관: **"어둠 속의 빛(Light in the Dark)"**. Dark BG + 아주 작은 별빛 + 어둠 속 빛(웜 골드). 주인공은 콘텐츠(가장 밝게), 연출은 절제.
- 서비스명: **Glim**.
- 핵심 토큰: `--bg0:#03050B` `--gold:#FFB25A` `--blue:#5B8CFF` `--cyan:#8FD3FF`, 세리프=Fraunces(italic 강조), 산세리프 본문, 글래스모피즘.
- 상세: `04_브랜딩_branding/세계관_v2_빛_컨셉.md`, `세계관_v2_빛_비주얼.html`, `03_UX디자인_ux/디자인_시스템.md`·`디자인_테마.md`.

## 3. 지금까지 상태
- **시나리오 1 (완료·배포):** "The Hard Landing on Mars" 다크 학습씬.
  - 파일(작업 기준): **`03_UX디자인_ux/Glim_POC_LearningFlow_EN.html`** ← 앞으로도 EN 파일이 기준. 한글판 `Glim_POC_학습플로우.html`은 보존만.
  - 흐름: 세션 picker → Mars 카드 클릭 → 다크 학습씬(문장 순차 노출 + 하이라이트) → 하단 좌측 ✦별 탭 → 사용자 발화(STT 단어단위) → 1.5s 후 Agent 소크라틱 응답(fade) + 발화 축소·상단이동 → Progress steps → 완료 시 **파티클 축하 + 학습 리포트**.
  - **라이브:** https://keanyyoon.github.io/AAL/ (GitHub Pages, repo `keanyyoon/AAL`, `prototype/` 폴더 = 배포본). `git push` 시 자동 반영.
- **시나리오 2 (기획 완료, 구현 대기):** "Inside Idol Culture" (K-pop 아이돌 문화).
  - 기획문: **`03_UX디자인_ux/POC_시나리오2_Kpop_Flow.md`** ← 다음 작업의 스펙.

## 4. 다음 작업 = 시나리오 2 HTML 구현
기획문(위 파일) 기준. 요약:
1. 학습목록에 **"Inside Idol Culture"** 카드 추가.
2. 클릭 시 다크→**밝은 종이(Paper) 테마**로 "빛이 지면으로 확장되는" 전환. (`--paper:#F5F0E6`, `--ink:#2A2620`, 미세 결 texture)
3. **지문 + 인포그래픽(3-pillar: Training·Rituals·Belonging) 인라인 SVG**, 이미지 hotspot 탭 인터랙션.
4. **크로스모달 문항**(문장 ↔ 이미지 기둥 연결) + 소크라틱 turn(의미→논리→추론).
5. **Unhappy path:** 학습자가 발화로 "하기 싫어/그만할래" → Agent가 감정 인정 → 진행 상기 → `계속/쉬기/저장` 선택지. **다크패턴 금지**(자율·존중).
- 권장: 신규 파일 `03_UX디자인_ux/Glim_POC_Scenario2_Kpop_EN.html` (테마 충돌 방지). 시나리오1의 음성대사·progress·파티클·리셋 로직 재사용.

## 5. 작업 규칙 (중요)
- **모든 텍스트 영문**, 사용자명 "Youngmin".
- **재사용 패턴:** 하단 음성 대사(별 탭→STT 단어단위→Agent 1.5s fade→발화 축소), Progress steps(원 크기 통일, `.is-done` 체크), 완료 리포트+파티클.
- **이미지 자산:** 외부 파일 의존 최소화(인라인 SVG 선호). 시나리오1 자산=`card001.jpeg`/`mars_bg.jpg`/`moon.jpeg`(HTML과 같은 폴더).
- **배포 반영:** 변경 후 `prototype/` 폴더 동기화하고 `git push` → 라이브 자동 갱신.
- 실수하면 재발 방지 위해 관련 `.md`에 기록.

## 6. 열린 결정 (구현 전 확인)
- 지문 톤: 팬덤 밝은 면 중심 vs 비판적 관점(압박·과열) 소폭 포함 여부.
- unhappy-path 선택지 3개 최종 문구.
- 시나리오2: 별도 파일 vs 기존 파일 씬 확장(별도 파일 권장).

---
### 붙여넣기용 시작 프롬프트 (새 세션에 그대로)
> "Glim POC 이어서 작업할게. 먼저 `03_UX디자인_ux/HANDOVER.md`와 `POC_시나리오2_Kpop_Flow.md`를 읽고, 시나리오 1 파일 `Glim_POC_LearningFlow_EN.html`의 구조·톤을 파악해줘. 그다음 시나리오 2(아이돌 문화, 밝은 종이 테마 + 이미지 hotspot + 음성 이탈 방지)를 새 EN HTML로 구현하자. 시작 전에 6번 열린 결정만 나에게 확인해줘."
