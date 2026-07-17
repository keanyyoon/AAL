# POC 시나리오 2 — "Inside Idol Culture" (Light/Paper 리딩 씬)

작성일: 2026-07-13 · 기준(향후 구현): `03_UX디자인_ux/` 신규 EN HTML
전제: 시나리오 1(Mars, 다크 씬) 구조·인터랙션을 재사용하되 **밝은 종이(Light/Paper) 테마 + 텍스트·이미지 크로스모달 상호작용 + 음성 이탈 방지(unhappy path)**를 신규 추가.
소재: **K-pop 아이돌 문화** (세계화의 동력을 '아이돌–팬덤 문화'로 풀어냄).

---

## 0. 설계 목표 & 세계관 정합성

- **문해력 축:** 의미(Meaning) · **논리(Logic)** · **추론(Inference)**. 텍스트의 주장과 이미지의 시각 근거를 연결하는 크로스모달 추론이 차별점.
- **세계관("어둠 속의 빛") 정합:** *"몰입해 읽는 순간 콘텐츠 자체가 빛이 되어 화면을 채운다"* → 다크→라이트(종이) 전환을 "빛이 지면으로 확장되는" 연출로 프레이밍. Agent orb는 라이트 테마에서도 웜 골드 광점 유지.
- **소재 선정 이유:** 아이돌 문화는 11~15세 글로벌 학생의 높은 공감대 + "왜 수백만이 개인적 유대를 느끼는가?"라는 **추론 질문**으로 자연스럽게 이어져 문해력 훈련에 적합. 팬덤의 밝은 면(소속감·성장 서사)을 중심으로 다루되 균형 잡힌 톤 유지(연령 적합).

---

## 1. Scene A — 학습목록에 아이돌 문화 카드

- 위치: `Explore More` 캐러셀 맨 앞(또는 Today's Picks 보조 카드).
- 카드 스펙(다크 카드 톤 유지, 썸네일만 비비드):
  - Title: **"Inside Idol Culture."**
  - Field: `Culture & Media · Meaning · Logic · ~10 min`
  - 난이도 별 3/5, Exp. +9
  - 아이콘/썸네일: 🎤 / 응원봉(light stick) 모티프(웜톤 위 네온 포인트)
- 클릭 → Scene B 진입(테마 전환 트랜지션).

---

## 2. Transition — Dark → Light(Paper)

- 클릭 시 1.0~1.4s: 다크 배경 위로 **종이 지면이 위에서 아래로 "켜지듯"(unfurl/fade)** 덮인다.
- Paper 테마 토큰(안):
  - `--paper:#F5F0E6`(크림), `--paper2:#EFE7D7`(음영), 미세 결 texture(SVG feTurbulence/반복배경)
  - `--ink:#2A2620`(본문), `--ink-soft:#6A6152`(캡션)
  - accent: `--gold:#FFB25A`, 하이라이트 `rgba(255,178,90,.22)`
  - Agent orb: 웜 골드 광점 유지
- 상단 Progress·⚙Settings·Previous 는 Mars 씬과 동일 배치, 색만 라이트용(잉크/골드).

---

## 3. Scene B — 지문 + 이미지 레이아웃 (매거진/징 스타일)

```
[ Progress ····· ⚙ ]
 Headline (serif)
 ┌───────────── 인포그래픽 이미지(3-pillar) ─────────────┐
 │  The Training  /  The Rituals  /  The Belonging       │
 │  (각 pillar = 탭 가능한 hotspot)                       │
 └────────────────────────────────────────────────────────┘
 본문 지문(문장 단위 순차 reveal + 하이라이트 구절)
 [ Question 패널 ]
 ──────────── 하단 음성 대사(별 탭→발화→Agent) ────────────
```

### 3-1. 지문(초안, EN) — 아이돌 문화
> **Inside Idol Culture**
>
> (P1) A K-pop "idol" is more than a singer. Most **train for years** — in singing, dancing, and even foreign languages — before they ever debut. By the time they first step on stage, many fans feel they have **watched them grow up**.
>
> (P2) Around each group, fans build a culture of their own. Every fandom has its **own name, an official light stick, and fan chants** shouted at the exact right moment in a song. These shared signals turn a crowd of strangers into a single community.
>
> (P3) So the strong bond fans feel is not an accident. It grows from years of visible effort and from rituals that let fans **belong to something bigger than themselves.** Idol culture offers not only music, but a feeling of belonging.

- 문장 단위 `.sent` 순차 노출(Mars 동일).
- 하이라이트 id: `k-train`, `k-ritual`, `k-grow`, `k-belong` (처음 숨김 → turn 진행 시 reveal).

### 3-2. 이미지 인터랙션 (핵심 신규 요소)
- 이미지 = **3-pillar 인포그래픽**: `The Training`(연습생 기간) / `The Rituals`(응원봉·팬챈트·팬덤명) / `The Belonging`(소속감). 인라인 SVG + 좌표 hotspot 권장(저작권 안전).
- hotspot 탭 → 마이크로 캡션 팝(예: Rituals = "Name · Light stick · Chant") + 대응 본문 하이라이트 동시 점등(크로스모달 연결 시각화).
- **크로스모달 문항:** "이 문장과 짝이 되는 그림 속 기둥을 골라봐" → 이미지 hotspot 탭으로 답.

### 3-3. 문항/Socratic turn (Happy path)
- **Q1 (의미):** "아이돌은 데뷔 전에 무엇을 오래 하지?" → 발화 → Agent 근거 유도 → `k-train` reveal.
- **Q2 (크로스모달·논리):** "'팬덤 이름·응원봉·팬챈트' 문장은 그림 어느 기둥?" → 이미지 `Rituals` hotspot 탭 → `k-ritual` reveal, setStep.
- **Q3 (추론):** "그럼 팬들의 강한 유대감은 '노래' 때문만일까?" → 추론 발화 → Agent `k-belong`+`k-grow` reveal, 결론 도출 → finish + 리포트/파티클(Mars 연출 재사용).

---

## 4. Unhappy Path — 음성 이탈("문제 풀기 싫어") 붙잡기

**트리거:** 문제 풀이 중(예: Q2 시점) 학습자가 별을 탭하고 **"근데 나 이거 하기 싫어 / 그만할래"** 류의 이탈 의사를 발화. (실서비스: ASR 위 intent 분류 / POC: 스크립트된 turn으로 시연)

**설계 원칙(다크패턴 금지):** 감정 인정 → 자율성 존중 → 부담 낮추기 → 궁금증. 죄책감 유발·강제 잔류·거짓 손실 경고 배제.

**Agent 재참여 플로우:**
1. **인정(validate):** "괜찮아 — 이 지문 좀 길긴 했어." (감정 부정 X)
2. **재프레이밍 + 진행 상기(soft):** "사실 3개 중 2개는 벌써 풀었어. 마지막 하나만 같이 볼까, 아니면 잠깐 쉴까?"
3. **선택지(자율 존중):** `계속 (딱 한 문제)` / `잠깐 쉬기` / `저장하고 나가기`
   - **계속 →** 난이도 낮춘 **contingent 스캐폴딩**(쉬운 발문 + 힌트 선노출)으로 성공 경험 → flow 회복 → 긍정 마무리(peak-end).
   - **잠깐 쉬기 →** "좋아, 이따 이어서 하자"(부드러운 복귀 안내).
   - **저장하고 나가기 →** "오늘 얻은 빛(★2)은 안전하게 저장했어. 또 보자!"(죄책감 없이 종료).
4. **궁금증 후킹(선택 유도, 강요 X):** "왜 낯선 사람 수천 명이 한 순간 '우리'가 되는지… 답이 바로 다음 장에 있어."

**측정 포인트(향후):** 이탈 발화 후 잔류율 / 재참여 후 완료율 / '쉬기→복귀'율.

---

## 5. 재사용 vs 신규 (기술 메모)

- **재사용:** 세션 picker, 하단 음성 대사(별 탭→STT 단어단위→Agent 1.5s fade), Progress steps, 완료 리포트+파티클, 리셋 로직.
- **신규:** Paper 라이트 테마 토큰/트랜지션, 이미지 hotspot 인터랙션, 크로스모달 문항, unhappy-path 분기(선택지 UI + 스크립트).
- **파일:** 신규 `03_UX디자인_ux/Glim_POC_Scenario2_Kpop_EN.html` 권장(테마 충돌 방지). 이미지=인라인 SVG(외부 파일 의존 최소화).

---

## 6. 확정 필요/열린 항목

- 이미지: 실제 아이돌 사진(저작권) 대신 **추상 3-pillar 인라인 SVG**로 제작 — OK?
- unhappy-path 선택지 3개 문구/톤 최종 확정.
- 지문 톤: 팬덤의 밝은 면 중심(현안). 압박/과열 등 비판적 관점도 살짝 넣을지 여부.
- 별도 파일 vs 기존 파일 씬 확장 — 별도 파일 권장.
