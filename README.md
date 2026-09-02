# AquaGarden Bench

같은 요구사항 하나를 서로 다른 AI 모델에게 주고 받은 **브라우저 전용 3D 수족관** 다섯 개를,
한 페이지에서 골라 실행하고 비교하는 갤러리입니다.

**라이브**: https://outliner-coach.github.io/aquagarden-bench/

---

## 공통 요구사항

다섯 버전 모두 같은 프롬프트와 같은 참고 사진 한 장에서 나왔습니다.
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

| # | 모델 | 도구 | 날짜 | 크기 | three.js | 원본 저장소 |
|---|---|---|---|---|---|---|
| 01 | GPT-5 | ChatGPT Canvas | 2025-08-09 | 24 KB · 345줄 | 0.161.0 | [aquagarden](https://github.com/outliner-coach/aquagarden) |
| 02 | Codex | OpenAI Codex CLI | 2026-03-05 | 98 KB · 3,116줄 | 0.161.0 | [aquagarden_codex](https://github.com/outliner-coach/aquagarden_codex) |
| 03 | Gemini Flash 3.5 | 단일 파일 프로토타입 | 2026-05-20 | 49 KB · 1,066줄 | 0.128.0 | [aquagarden_gemini_flash_3.5](https://github.com/outliner-coach/aquagarden_gemini_flash_3.5) |
| 04 | ox Alpha - GLM 5.3 | OpenCode | 2026-08-23 | 47 KB · 1,153줄 | 0.185.1 | [aquagarden_omo](https://github.com/outliner-coach/aquagarden_omo) |
| 05 | Claude Fable 5.1 | Claude Code | 2026-09-02 | 100 KB · 2,301줄 | 0.170.0 | 이 저장소 |

각 파일은 원본 저장소에서 **수정 없이 그대로** 복사했습니다.
05번만 이 저장소에서 처음 만들어졌습니다.

제외한 것: `aquagarden-for-builder`(요청에 따라), `aquascape`(React 다중 파일이라 단일 HTML이 아님).

---

## 구조

```
index.html                              갤러리 (수조 · 비교표 · 프롬프트)
assets/reference.jpg                    다섯 버전이 공유한 참고 이미지
versions/gpt-canvas/index.html          01
versions/codex/index.html               02
versions/gemini-flash-3-5/index.html    03
versions/glm-5-3/index.html             04
versions/claude-fable-5-1/index.html    05
```

갤러리는 선택한 버전 **하나만** iframe으로 불러옵니다.
다섯 개 모두 WebGL 씬이라 동시에 띄우면 GPU가 버티지 못합니다.

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

**기법** 표는 각 파일을 정적 분석해 확인한 렌더링 기법입니다.
같은 효과를 다른 이름으로 직접 구현한 경우는 잡히지 않으므로,
표시가 없다고 해서 그 기능이 없다는 뜻은 아닙니다.

---

## 05번 버전에 대하여

Claude Code(Fable 5.1)로 만든 버전입니다. 자세한 내용은
[versions/claude-fable-5-1/README.md](versions/claude-fable-5-1/README.md) 를 보세요.

- 유목·바위·수초·바닥 모두 절차적 생성. 외부 이미지도 `fetch` 도 없습니다.
- 물고기 5종 20마리(베타·플래티·네온테트라·코리도라스·구피)가 종별 수심대를 지키며 유영합니다.
- 수초 흔들림과 물고기 굴신은 `onBeforeCompile` 로 주입한 버텍스 셰이더가 처리합니다.
- 조명 프리셋 4종(주광·석양·달빛·RGB)과 밝기·색온도·물 색조 슬라이더.
- 13개 오브젝트 그룹에 각각 5~6개의 한국어 명언.
