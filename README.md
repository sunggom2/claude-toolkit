# claude-toolkit

개인 Claude Code 도구 모음(플러그인 마켓플레이스). 회사 PC·집 PC·클라우드 세션 어디서든 같은 스킬과 MCP 설정을
쓰려고 만든 저장소다.

> **공개 저장소다.** 회사 자료, 비밀번호·API 키, 회사 전용으로 고친 스킬은 넣지 않는다.

## 들어 있는 것

| 플러그인 | 내용 | 원본 (가져온 판) |
|---|---|---|
| `archify` | 아키텍처·워크플로·시퀀스·데이터 흐름·상태 다이어그램을 HTML 한 파일로 만드는 스킬 1개 | [tt-a1i/archify](https://github.com/tt-a1i/archify) `9e35d2b` (MIT) |
| `taste-skill` | 프론트엔드 디자인 스킬 13개 (아래 표) | [leonxlnx/taste-skill](https://github.com/leonxlnx/taste-skill) `c184364` (MIT) |
| `playwright` | Playwright 브라우저 자동화 MCP 서버 — macOS·Linux·클라우드 세션용 | [microsoft/playwright-mcp](https://github.com/microsoft/playwright-mcp) (Apache-2.0) |
| `playwright-windows` | 같은 서버, Windows PC용 (`cmd /c npx`로 실행) | 〃 |

- 스킬 파일은 원본을 **그대로** 복사했다. 바꾼 곳은 archify `SKILL.md` 의 「Update awareness」 절 하나뿐이다
  (원본은 다이어그램마다 묻지 않고 제작자 사이트에 새 판을 확인하고 그 사실을 말하지 말라고 한다 → 확인하지 않도록 바꿈).
- Playwright 는 코드를 담지 않고 설정만 둔다. 실행할 때마다 `npx @playwright/mcp@latest` 로 최신판을 받는다.

### taste-skill 13개

| 스킬(폴더) | 용도 |
|---|---|
| `taste-skill` | 랜딩 페이지·포트폴리오용 디자인 스킬(v2). 관리자 화면·대시보드는 스스로 범위 밖이라고 한다 |
| `taste-skill-v1` | taste-skill 옛 판(하위 호환용) |
| `gpt-tasteskill` | GPT 계열 모델용 강한 디자인 프롬프트(어워드풍 랜딩 페이지) |
| `redesign-skill` | 기존 사이트를 점검한 뒤 기능을 깨지 않고 단계적으로 다듬는 리디자인 지침 |
| `soft-skill` | 부드럽고 "비싸 보이는" 에이전시풍 UI |
| `minimalist-skill` | Notion·Linear 풍 흑백 에디토리얼 UI |
| `brutalist-skill` | 스위스 인쇄물·터미널 감성의 브루탈리즘 UI |
| `output-skill` | 코드를 `// ...` 로 생략하지 않고 끝까지 출력하게 하는 지침 |
| `image-to-code-skill` | 섹션별 시안 이미지를 먼저 만들고 그대로 코드로 옮김 (이미지 생성 도구 필요) |
| `imagegen-frontend-web` | 웹 시안 이미지를 섹션마다 생성 (코드 아님, 이미지 생성 도구 필요) |
| `imagegen-frontend-mobile` | 모바일 앱 화면 시안 이미지 생성 (코드 아님, 이미지 생성 도구 필요) |
| `brandkit` | 로고·색·글꼴을 한 장에 담은 브랜드 키트 이미지 프롬프트 (이미지 생성 도구 필요) |
| `stitch-skill` | Google Stitch 에 넣을 `DESIGN.md` 작성 |

## PC에 설치 (컴퓨터마다 한 번)

Claude Code 안에서:

```
/plugin marketplace add sunggom2/claude-toolkit
/plugin install archify@claude-toolkit
/plugin install taste-skill@claude-toolkit
/plugin install playwright@claude-toolkit            # macOS·Linux
/plugin install playwright-windows@claude-toolkit    # Windows
```

터미널에서는 같은 일을 `claude plugin marketplace add sunggom2/claude-toolkit`,
`claude plugin install archify@claude-toolkit` … 로 한다.

- Playwright 는 Node.js 가 있어야 하고 PC 에 설치된 Google Chrome 을 쓴다.
- 이 저장소를 고친 뒤 PC 에 반영: `/plugin marketplace update claude-toolkit` → `/plugin update <플러그인>@claude-toolkit`.
  플러그인 내용을 바꿀 때는 그 플러그인의 `.claude-plugin/plugin.json` `version` 을 올린다.

## 클라우드 세션(claude.ai/code)에서

클라우드 세션은 매번 새 컨테이너라 PC 설치가 따라오지 않는다. 클라우드 환경 설정(세션 제목줄의 환경 메뉴 → 편집)에 넣는다.

설정 스크립트:

```bash
claude plugin marketplace add sunggom2/claude-toolkit
claude plugin install archify@claude-toolkit
claude plugin install taste-skill@claude-toolkit
claude plugin install playwright@claude-toolkit
```

환경 변수 (컨테이너에는 Chrome 도 화면도 없어서, 미리 깔린 Chromium 을 화면 없이 쓰게 한다):

```
PLAYWRIGHT_MCP_BROWSER=chromium
PLAYWRIGHT_MCP_EXECUTABLE_PATH=/opt/pw-browsers/chromium
PLAYWRIGHT_MCP_HEADLESS=true
PLAYWRIGHT_MCP_OUTPUT_DIR=/tmp/playwright-mcp
```

## 회사 작업에 쓸 때 주의

들이기 전에 전부 읽고 검토했다(2026-09-24). 스킬 안에 제작자 크레딧·제휴 링크·숨은 지시는 없었다
(taste-skill 원본 README 의 제휴 링크는 가져오지 않았다). 다만:

- **taste-skill 여러 개가 자리표시 사진을 `picsum.photos` 같은 외부 사이트에서 불러오는 코드를 만든다.**
  사내 화면에 그대로 두면 페이지를 열 때마다 외부로 요청이 나간다 → 회사 작업에서는 "외부 이미지·CDN 쓰지 말고
  빈 자리표시로" 라고 함께 말한다.
- `taste-skill` 은 이미지 생성 도구가 연결돼 있으면 반드시 쓰라고 한다. 이미지 생성 계열 스킬과 `stitch-skill` 은
  화면 설명을 외부 서비스(이미지 생성, Google Stitch)로 보낸다 → 회사 내용이면 쓰지 않거나 먼저 확인한다.
- 추천 글꼴 가운데 상용 글꼴(PP Editorial New, Söhne 등)이 있다 → 쓰기 전에 라이선스 확인.
- archify: 사용자가 공식 주소를 준 브랜드 아이콘만 그 사이트에서 받아 온다. 그린 뒤 결과 파일 옆에 스크린샷(PNG·JSON)을
  남기므로 결과는 git 에서 뺀 폴더에 만든다.

## 원본 새 판으로 바꾸기

- archify:
  ```bash
  npx skills add tt-a1i/archify -g
  rm -rf plugins/archify/skills/archify && cp -r ~/.agents/skills/archify plugins/archify/skills/archify
  ```
  `SKILL.md` 의 「Update awareness」 절을 다시 이 저장소 안내로 바꾸고, 표의 커밋과 `plugin.json` `version` 을 고친다.
- taste-skill:
  ```bash
  git clone --depth 1 https://github.com/leonxlnx/taste-skill /tmp/taste-skill
  rm -rf plugins/taste-skill/skills && cp -r /tmp/taste-skill/skills plugins/taste-skill/skills
  cp /tmp/taste-skill/LICENSE plugins/taste-skill/LICENSE
  ```
  표의 커밋과 `plugin.json` `version` 을 고친다.
- Playwright: 할 일 없음 (늘 최신판).

## 라이선스

각 원본의 라이선스를 따른다: `plugins/archify/skills/archify/LICENSE`, `plugins/taste-skill/LICENSE` (둘 다 MIT).
Playwright MCP(Apache-2.0)는 코드를 담지 않고 실행 설정만 둔다.
