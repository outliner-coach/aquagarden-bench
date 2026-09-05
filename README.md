# AquaGarden Bench

같은 요구사항 하나를 서로 다른 AI 모델에게 주고 받은 **브라우저 전용 3D 수족관** 열 개를,
한 페이지에서 골라 실행하고 비교하는 갤러리입니다.

**라이브**: https://outliner-coach.github.io/aquagarden-bench/

---

## 공통 요구사항

열 버전 모두 같은 프롬프트와 같은 참고 사진 한 장에서 출발했습니다.
다만 **제작 조건은 서로 다릅니다** — 아래 「제작 조건」 절을 먼저 봐주세요.
갤러리의 **프롬프트** 탭에서 원문과 이미지를 나란히 볼 수 있고,
원문 파일은 [prompt.md](https://github.com/outliner-coach/aquagarden_gemini_flash_3.5/blob/main/prompt.md) 에 있습니다.

> 브라우저만으로 실행 가능한 3D 디지털 수족관을 만들어줘.
>
> **배경** — 수초와 유목, 바위들로 이루어져 있다. 첨부한 이미지를 참고하여 3D로 디자인한다.
> 수초는 자연스럽게 흔들린다. 공기 기포가 자연스럽게 올라온다.
>
> **물고기** — 3종류 이상. 자유롭게 유영하며 수족관을 돌아다닌다.
> 지느러미와 꼬리가 자연스럽게 움직인다.
>
> **기능** — 사용자는 조명을 조절할 수 있다.
> 오브젝트들을 클릭하면 각 오브제와 관련된 명언이 나온다.

---

## 수록된 버전

| # | 모델 | 도구 | 날짜 | 크기 | three.js | 원본 |
|---|---|---|---|---|---|---|
| 01 | GPT-5 | ChatGPT Canvas | 2025-08-09 | 24 KB · 345줄 | 0.161.0 | [aquagarden](https://github.com/outliner-coach/aquagarden) |
| 02 | Gemini 3 | Antigravity | 2025-11-19 | 1.4 MB · React 빌드 | 0.181.2 | [aquascape](https://github.com/outliner-coach/aquascape) |
| 03 | Opus 4.6 | Claude Code | 2026-02-22 | 48 KB · 1,226줄 | 0.160.0 | Slack |
| 04 | Codex 5.3 exhigh | Codex | 2026-02-22 | 40 KB · 1,303줄 | 0.161.0 | Slack |
| 05 | Gemini 3.1 Pro | Antigravity | 2026-02-22 | 38 KB · 1,078줄 | 0.128.0 | Slack |
| 06 | Codex | OpenAI Codex CLI | 2026-03-05 | 98 KB · 3,116줄 | 0.161.0 | [aquagarden_codex](https://github.com/outliner-coach/aquagarden_codex) |
| 07 | Gemini Flash 3.5 | 단일 파일 프로토타입 | 2026-05-20 | 49 KB · 1,066줄 | 0.128.0 | [aquagarden_gemini_flash_3.5](https://github.com/outliner-coach/aquagarden_gemini_flash_3.5) |
| 08 | ox Alpha - GLM 5.3 | OpenCode | 2026-08-23 | 47 KB · 1,153줄 | 0.185.1 | [aquagarden_omo](https://github.com/outliner-coach/aquagarden_omo) |
| 09 | Claude Fable 5.1 | Claude Code | 2026-09-02 | 100 KB · 2,301줄 | 0.170.0 | 이 저장소 |
| 10 | GPT-6 Astra | OpenAI Codex · xhigh | 2026-09-05 | 47 KB · 546줄 | 0.170.0 | 이 저장소 |

01·06·07·08 은 원본 저장소에서, 03·04·05 는 사내 슬랙에 공유된 첨부 파일에서
**수정 없이 그대로** 가져왔습니다. 02 는 `gh-pages` 빌드를 그대로 받아
자산 경로만 상대 경로로 고쳤습니다. 09·10 은 이 저장소에서 처음 만들어졌습니다.

02 를 뺀 아홉 개는 HTML 파일 하나로 끝나고, 02 만 React 빌드라 번들이 함께 들어 있습니다.

제외한 것: `aquagarden-for-builder`(요청에 따라).

---

## 구조

```
index.html                                  갤러리 (수조 · 비교표 · 프롬프트)
assets/reference.jpg                        열 버전이 공유한 참고 이미지
versions/gpt-canvas/index.html              01
versions/gemini-3-antigravity/              02  React 빌드 (index.html + assets/)
versions/opus-4-6/index.html                03
versions/codex-5-3/index.html               04
versions/gemini-3-1-pro/index.html          05
versions/codex/index.html                   06
versions/gemini-flash-3-5/index.html        07
versions/glm-5-3/index.html                 08
versions/claude-fable-5-1/index.html        09
versions/Gpt 6 astra/index.html            10
```

갤러리는 선택한 버전 **하나만** iframe으로 불러옵니다.
각 버전이 WebGL 씬이라 동시에 실행하면 GPU 부하가 커집니다.

각 버전은 독립 실행됩니다. `versions/<이름>/index.html` 을 직접 열어도 그대로 동작합니다.

---

## 로컬에서 실행

```bash
python3 -m http.server 8790
```

브라우저에서 <http://localhost:8790> 을 엽니다.
빌드 과정은 없고, three.js 는 각 파일이 CDN에서 직접 불러옵니다.
`#claude-fable-5-1` 처럼 해시를 붙이면 특정 버전으로 바로 열립니다.

---

## 비교표에 대하여

**규모** 표의 파일 크기와 줄 수는 배포된 파일에서 직접 잰 값이고, 날짜는 원본 저장소의 커밋 날짜입니다.

**기법** 표는 각 버전의 코드를 직접 읽어 판정했습니다.
이름이 아니라 실제 동작 기준입니다. 예를 들어 코스틱은 바닥에 무늬를 드리우는 경우만 인정하고
물속에 떠 있는 광선 기둥(`addCaustics` 라는 이름을 쓰더라도)은 제외했으며,
군영은 결속·정렬·분리 중 둘 이상을 이웃과 계산하는 경우만 인정했습니다.
`boid` 라는 단어를 한 번도 쓰지 않고 세 규칙을 다 구현한 파일이 있어, 키워드 검색으로는 판정할 수 없었습니다.

---

## 제작 조건 — 같은 조건이 아닙니다

**열 개가 모두 프롬프트 한 번으로 나온 것은 아닙니다.**
한 번에 끝난 것과 몇 시간 고쳐가며 만든 것을 나란히 놓고 우열을 가릴 수는 없으니,
아래를 전제로 나머지 표를 봐주세요.

| # | 모델 | 제작 방식 | 비고 |
|---|---|---|---|
| 01 | GPT-5 | **반복 수정** | SVG 로 시작했다가 3D 로 갈아엎었고, 프롬프트를 여러 번 고쳐 v4 까지 갔습니다 |
| 02 | Gemini 3 | **반복 수정** | 세 시간 가까이. 도중에 Gemini 과부하 오류로 **Claude Sonnet 4.5 thinking 으로 바꿔 이어서** 작업 |
| 03 | Opus 4.6 | 원 프롬프트 | 같은 날 3종 동시 비교. 셋 중 가장 오래 걸림 |
| 04 | Codex 5.3 exhigh | 원 프롬프트 | 같은 날 3종 동시 비교 |
| 05 | Gemini 3.1 Pro | 원 프롬프트 | 같은 날 3종 동시 비교. 약 10분 |
| 06 | Codex | **반복 수정** | 계획서와 진행 기록을 남기며 여러 커밋에 걸쳐 다듬음 |
| 07 | Gemini Flash 3.5 | 확인 안 됨 | 기록 없음 |
| 08 | ox Alpha - GLM 5.3 | 확인 안 됨 | 기록 없음 |
| 09 | Claude Fable 5.1 | 원 프롬프트 + 보완 1회 | 만든 뒤 참고 사진과 대조해 하드스케이프와 수초를 한 차례 다듬음 |
| 10 | GPT-6 Astra | 원 프롬프트 + 실행 검증 | 공통 원문·사진으로 구현하고 브라우저 검증 및 필요한 보정을 수행. 무수정 단일 응답 측정은 아님 |

특히 **02 는 순수 Gemini 3 결과물로 보기 어렵습니다.** 중간에 모델을 갈아탔습니다.

## 요구사항을 다 지켰는가

각 버전의 코드와 브라우저 동작을 확인한 결과, **두 번은 요구사항을 빠뜨렸습니다.**

| 모델 | 물고기 3종 이상 | 조명 조절 | 클릭 명언 |
|---|---|---|---|
| GPT-5 | 3종 53마리 | **없음** | 있음 |
| Gemini 3 | 4종 25마리 | 밝기 하나 | **없음** |
| Opus 4.6 | 5종 22마리 | 있음 | 있음 |
| Codex 5.3 exhigh | 3종 29마리 | 있음 | 있음 |
| Gemini 3.1 Pro | 5종 19마리 | 있음 | 있음 |
| Codex | 3종 16마리 | 있음 | 있음 |
| Gemini Flash 3.5 | 3종 10마리 | 있음 | 있음 |
| ox Alpha - GLM 5.3 | 4종 18마리 | 있음 | 있음 |
| Claude Fable 5.1 | 5종 20마리 | 있음 | 있음 |
| GPT-6 Astra | 5종 24마리 | 있음 | 있음 · 창작 문장 |

- **GPT-5** — 파일 전체에 `<input>` 도 `<button>` 도 하나 없습니다. 조명 UI 자체를 만들지 않았습니다.
- **Gemini 3 / Antigravity** — 씬 위 여섯 지점을 클릭해봤지만 DOM 이 전혀 변하지 않고,
  번들 어디에도 한국어 문자열이 없습니다. 명언 상태를 담을 스토어는 만들어놨지만 아무도 호출하지 않습니다.

물고기 종 수는 열 개 모두 통과했습니다.

## 알려진 특이사항

원본을 그대로 두는 게 벤치마크의 요점이라, 아래는 **고치지 않고 남겨둔 것들**입니다.
모두 화면에는 영향이 없고 콘솔에서만 보입니다.

- **08 ox Alpha - GLM 5.3** — 로딩 직후 `GL_INVALID_FRAMEBUFFER_OPERATION` 경고가 100개 가까이 쏟아집니다.
  `renderer.setSize` 를 iframe 의 실제 크기가 잡히기 전에 부르는 탓으로 보이며,
  로딩 화면이 3~11초로 들쭉날쭉합니다. 결국에는 정상적으로 렌더링됩니다.
- **01 GPT-5** — 자체 `console.assert` 가 매번 실패합니다
  ("몸통에 onBeforeCompile 셰이더가 적용되어야 합니다"). 화면은 의도대로 나옵니다.
- **07 Gemini Flash 3.5** — Tailwind 를 CDN 스크립트로 불러와 프로덕션 경고가 뜹니다.
- **02 Gemini 3 / Antigravity** — 번들이 1.4 MB 라 첫 렌더까지 몇 초 걸립니다.

## 09번 버전에 대하여

Claude Code(Fable 5.1)로 만든 버전입니다. 자세한 내용은
[versions/claude-fable-5-1/README.md](versions/claude-fable-5-1/README.md) 를 보세요.

- 유목·바위·수초·바닥 모두 절차적 생성. 외부 이미지도 `fetch` 도 없습니다.
- 물고기 5종 20마리(베타·플래티·네온테트라·코리도라스·구피)가 종별 수심대를 지키며 유영합니다.
- 수초 흔들림과 물고기 굴신은 `onBeforeCompile` 로 주입한 버텍스 셰이더가 처리합니다.
- 조명 프리셋 4종(주광·석양·달빛·RGB)과 밝기·색온도·물 색조 슬라이더.
- 13개 오브젝트 그룹에 각각 5~6개의 한국어 명언.

## 10번 버전에 대하여

GPT-6 Astra(`xhigh`)로 공통 원문과 사진을 사용해 새로 만든 버전입니다.
[제작 조건과 구현·검증 기록](versions/Gpt%206%20astra/README.md)을 참고하세요.

- 왼쪽 유목·녹색 수초, 중앙 층진 바위, 오른쪽 붉은 수초를 절차적 3D로 구성.
- 베타·네온테트라·엠버테트라·허니구라미·코리도라스 5종 24마리.
- 조명 3종과 밝기·색온도 조절, 회전·확대·초기화, 일시정지와 전체 화면.
- 3D 오브젝트 클릭과 키보드 선택 메뉴로 볼 수 있는 9개의 창작 문장.
- 바로 실행: https://outliner-coach.github.io/aquagarden-bench/#gpt-6-astra
