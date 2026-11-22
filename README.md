<p align="center">
  <img src="assets/logo.svg" width="96" height="96" alt="wwt-lite logo">
</p>

<h1 align="center">wwt-lite</h1>

<p align="center">
  <b>An agent browser for Claude Code, Codex and other AI agents, where you can take the wheel at any time.</b>
</p>

<p align="center">
  <a href="https://github.com/d2wolab/wwt-lite-releases/releases/latest">Download</a> ·
  <a href="#install">Install</a> ·
  <a href="#try-it">Try it</a> ·
  <a href="#faq">FAQ</a> ·
  <a href="#한국어">한국어</a>
</p>

<!-- DEMO GIF: add assets/demo.gif here when the demo recording is ready.
<p align="center"><img src="assets/demo.gif" width="720" alt="An agent fills a form, a person takes over and edits, hands back, and the agent saves"></p>
-->

Your agent drives a real Chrome window on your computer. You watch, and whenever you want, press **Take over**, do it yourself, then press **Resume** to hand it back.

> **Status:** public beta, [v0.1.0-beta.1](https://github.com/d2wolab/wwt-lite-releases/releases/tag/v0.1.0-beta.1). Expect changes; please [report issues](https://github.com/d2wolab/wwt-lite-releases/issues).
>
> This repository hosts release downloads only (installers, one-line install scripts and checksums). Source code is not published here.

## Install

macOS:

```bash
curl -fsSL https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.sh | sh
```

Windows (PowerShell):

```powershell
irm https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.ps1 | iex
```

Then ask your agent: *"Use wwt-browser to open example.com and summarize the page."*

Needs macOS 13.5+ (Apple silicon) or Windows 10/11 (x64), and Google Chrome. No admin rights, no separate Node.js. [Details below.](#install-details)

## Why wwt-lite

- **You and the agent share one window.** The agent works; you can step in at any moment. A control bar in the window has **Take over**, **Resume** and a stop icon. While you are in control the agent waits, and when it reaches a sign-in or a step only you should do, it hands the window to you.
- **Calm on websites.** It runs the Chrome you already have installed, in its own profile, with human-paced mouse, scrolling and typing. It leaves site permissions at Chrome's defaults and is built not to pull its window in front of what you are doing. It does not solve CAPTCHAs; those are handed to you.
- **Works well with small, fast models.** The skill guide is short, and agents can read just the text or a list of items from a page instead of a huge page dump, so small, low-cost models such as Claude Haiku can do real tasks too.
- **Fits how you work.** A menu bar / tray app shows each agent window live, whether it is Running or in Manual mode, plus CPU and memory use. A local MCP server lets Claude desktop chat (and other MCP apps) use it too. The UI comes in 12 languages.

## Try it

Paste one of these into Claude Code, Codex or another agent after installing:

**Price check**

```text
Use wwt-browser to search an online shop for "wireless earbuds", and give me the
names and prices of the first 10 results as a table. If the site asks me to sign
in or verify anything, hand the window to me.
```

**Public data lookup**

```text
Use wwt-browser to open the World Bank open data site, find the population of
South Korea and Japan for the last 5 years, and give me a small table with the
source link.
```

**Web app QA**

```text
Use wwt-browser to open http://localhost:3000, sign-up flow first. Try an empty
form, an invalid email and a valid sign-up. Take a screenshot of each step and
list anything that looks broken.
```

While it works, try pressing **Take over**, change something yourself, then press **Resume**.

## Screenshots

<!-- SCREENSHOTS: add images to assets/ when ready, for example:
| Control bar | Menu bar app |
|---|---|
| <img src="assets/control-bar.png" width="360" alt="Control bar with Take over, Resume and stop"> | <img src="assets/menubar.png" width="360" alt="Menu bar app with live window thumbnails"> |
-->

_Coming soon._

## Tested

- Real-Chrome end-to-end test suite: **100% pass on macOS and Windows** on the current build.
- macOS builds are signed with an Apple Developer ID and notarized. Every download is checked against `SHA256SUMS` by the installer.

## Install details

The installer downloads the release for your system, checks its SHA-256 checksum against `SHA256SUMS`, and installs into your user folder (no administrator rights).

What gets installed:

| Item | macOS | Windows |
|---|---|---|
| `wwt-browser` command | `~/.local/bin/wwt-browser` | added to your user PATH |
| Engine and bundled Node | `~/Library/Application Support/wwt-lite/` | `%LOCALAPPDATA%\Programs\wwt-lite\` |
| Menu bar / tray app | `~/Applications/wwt-lite.app` | Start menu shortcut |
| Agent skill `wwt-browser` | `~/.agents/skills` (and `~/.claude/skills`, `~/.codex/skills` if those apps are installed) | same folders under your user profile |

Options: `--no-menubar` skips the menu bar / tray app (for example on a server), `--no-skills` skips the agent skill. On Windows use `-NoMenubar` and `-NoSkills`.

macOS builds are signed with an Apple Developer ID and notarized. Windows builds are not code-signed yet.

## Use with Claude Code, Codex and other agents

The installer adds the `wwt-browser` skill to your agents. Then just ask, for example:

> Use wwt-browser to open example.com and summarize the page.

Check that it works:

```bash
wwt-browser --version
wwt-browser skill
```

While the agent is in control, the Chrome window shows a control bar at the bottom. Press **Take over** to use the window yourself, **Resume** to hand it back, or the stop icon to end the task.

## Use in Claude desktop chat (MCP)

After installing, download `wwt-lite.mcpb` from the [latest release](https://github.com/d2wolab/wwt-lite-releases/releases/latest) and open it, or drag it into Claude desktop's **Settings → Extensions**. Claude can then browse with wwt-lite from a normal chat.

Other MCP apps can run the local server directly: command `wwt-browser`, arguments `mcp` (stdio). It runs on your computer only; there is no hosted server.

## Update

Run the same install command again, or:

```bash
wwt-browser upgrade
```

## Stop the engine

The engine starts when an agent needs it. To stop it, open the menu bar / tray app, then **⋯ → Quit** (or **Restart engine** if something is stuck).

## Uninstall

macOS:

```bash
curl -fsSL https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.sh | sh -s -- --uninstall
```

Windows (PowerShell):

```powershell
& ([scriptblock]::Create((irm https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.ps1))) -Uninstall
```

Your normal Chrome profile is never touched. wwt-lite uses its own browser profile.

## Verify a download manually

Each release includes `SHA256SUMS`. Compare it with:

```bash
shasum -a 256 <file>          # macOS
Get-FileHash <file> -Algorithm SHA256   # Windows PowerShell
```

## FAQ

**Is my everyday Chrome safe?**
Yes. wwt-lite starts Chrome with its own separate profile. Your normal profile, its cookies, history and saved passwords are never read or changed. You can keep using your everyday Chrome side by side.

**What about passwords?**
wwt-lite does not read, store or send passwords, cookies or tokens. When a site needs a sign-in, the agent hands the window to you and you type it yourself. You can also sign in once ahead of time with `wwt-browser setup`; that sign-in stays in wwt-lite's own profile on your computer.

**Is it free?**
Yes. The [license](LICENSE.md) lets you use it free of charge, for personal or commercial work.

**Windows shows a SmartScreen warning.**
Windows builds are not code-signed yet, so SmartScreen may warn about an unknown publisher. The installer checks every file against the published `SHA256SUMS`; you can also [verify a download manually](#verify-a-download-manually).

**Intel Mac or Linux?**
Not yet. The beta supports Apple silicon Macs (macOS 13.5+) and Windows 10/11 x64. Tell us in [issues](https://github.com/d2wolab/wwt-lite-releases/issues) if you need another platform.

**Does it send my data anywhere?**
No telemetry. Pages, screenshots and logs stay on your computer and go only to the agent you run yourself. See [Privacy](PRIVACY.md).

## License, security and privacy

- [License (EULA)](LICENSE.md): free to use; no modification, reverse engineering or redistribution.
- [Security](SECURITY.md): what wwt-lite does and does not do, and how to report a vulnerability.
- [Privacy](PRIVACY.md): no telemetry; everything stays on your computer.

---

## 한국어

**wwt-lite는 Claude Code, Codex 같은 AI 에이전트를 위한 브라우저입니다. 에이전트가 일하는 동안 사람이 언제든 핸들을 잡을 수 있습니다.**

에이전트가 내 컴퓨터의 실제 Chrome 창을 조작합니다. 지켜보다가 **Take over**(직접 하기)를 누르면 내가 직접 하고, **Resume**(다시 맡기기)을 누르면 에이전트에게 돌려줍니다. 이 저장소에는 설치 파일과 설치 스크립트만 있고 소스 코드는 없습니다.

> **상태:** 공개 베타 [v0.1.0-beta.1](https://github.com/d2wolab/wwt-lite-releases/releases/tag/v0.1.0-beta.1). 바뀔 수 있으니 문제가 있으면 [이슈](https://github.com/d2wolab/wwt-lite-releases/issues)로 알려 주세요.

**필요한 것:** macOS 13.5 이상(Apple 칩) 또는 Windows 10/11(x64), Google Chrome. Node.js는 함께 들어 있어 따로 설치하지 않아도 됩니다.

### 설치

macOS:

```bash
curl -fsSL https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.sh | sh
```

Windows (PowerShell):

```powershell
irm https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.ps1 | iex
```

설치기는 받은 파일의 SHA-256 지문을 `SHA256SUMS`와 비교한 뒤, 관리자 권한 없이 내 사용자 폴더에 설치합니다. `wwt-browser` 명령, 엔진, 메뉴 막대(트레이) 앱, 에이전트용 `wwt-browser` 스킬이 함께 설치됩니다. 메뉴 막대 앱이 필요 없으면 `--no-menubar`, 스킬이 필요 없으면 `--no-skills`를 붙이세요(Windows는 `-NoMenubar`, `-NoSkills`).

macOS 빌드는 Apple Developer ID로 서명하고 공증합니다. Windows 빌드는 아직 코드 서명이 없습니다.

### 왜 wwt-lite인가

- **사람과 에이전트가 한 창을 같이 씁니다.** 창 아래 제어 막대의 **Take over**·**Resume**·정지 아이콘으로 언제든 끼어들 수 있고, 내가 잡고 있는 동안 에이전트는 기다립니다. 로그인처럼 사람이 해야 할 단계에서는 에이전트가 창을 넘겨줍니다.
- **사이트에서 조용하게 움직입니다.** 이미 설치된 Chrome을 전용 프로필로 띄우고, 사람 속도의 마우스·스크롤·입력을 씁니다. 사이트 권한은 Chrome 기본값 그대로 두고, 하던 일 앞으로 창을 끌어오지 않게 만들었습니다. CAPTCHA는 풀지 않고 사람에게 넘깁니다.
- **작고 저렴한 모델로도 잘 돕니다.** 스킬 안내가 짧고, 페이지 전체 대신 필요한 글자나 목록만 읽을 수 있어서 Claude Haiku 같은 작은 모델도 실제 작업을 해냅니다.
- **쓰기 편합니다.** 메뉴 막대(트레이) 앱에서 에이전트 창을 실시간 썸네일과 Running/Manual 상태, CPU·메모리 사용량으로 봅니다. 로컬 MCP로 Claude 데스크톱 채팅에서도 쓸 수 있고, 화면은 12개 언어를 지원합니다.

### 이렇게 시켜 보세요

설치한 뒤 에이전트에게 붙여 넣어 보세요.

```text
wwt-browser로 쇼핑몰에서 "무선 이어폰"을 검색해서 첫 10개 상품의 이름과 가격을 표로 정리해 줘.
로그인이나 인증을 물으면 창을 나에게 넘겨줘.
```

```text
wwt-browser로 공공데이터포털(data.go.kr)에서 서울시 공공자전거 대여소 데이터를 찾아서
제공 기관, 갱신 주기, 내려받기 형식을 알려 줘.
```

```text
wwt-browser로 http://localhost:3000 회원가입 화면을 열어서 빈 칸 제출, 잘못된 이메일, 정상 가입을
차례로 해 보고, 단계마다 스크린샷을 찍어 깨진 곳을 알려 줘.
```

작업 중에 **Take over**를 눌러 직접 바꿔 보고, **Resume**으로 돌려줘 보세요.

### Claude 데스크톱 채팅에서 쓰기 (MCP)

설치한 뒤 [최신 릴리스](https://github.com/d2wolab/wwt-lite-releases/releases/latest)에서 `wwt-lite.mcpb`를 받아 열거나, Claude 데스크톱 **설정 → 확장**에 끌어다 놓으세요. 다른 MCP 앱에서는 명령 `wwt-browser`, 인자 `mcp`(stdio)로 실행합니다. 내 컴퓨터에서만 돌고 외부 서버는 없습니다.

### 쓰기·업데이트·끄기·삭제

- **Claude Code, Codex에서 쓰기:** 설치하면 스킬이 자동으로 등록됩니다. "wwt-browser로 example.com 열어서 요약해 줘"처럼 요청하면 됩니다. 확인: `wwt-browser --version`, `wwt-browser skill`.
- **업데이트:** 설치 명령을 다시 실행하거나 `wwt-browser upgrade`.
- **엔진 끄기:** 엔진은 에이전트가 쓸 때 자동으로 켜집니다. 끄려면 메뉴 막대(트레이) 앱의 **⋯ → 종료**, 멈춘 것 같으면 **엔진 다시 시작**.
- **삭제:** 위 영어 안내의 [Uninstall](#uninstall) 명령을 실행하세요. 평소 쓰는 Chrome 프로필은 건드리지 않습니다.
- **직접 검증:** 릴리스의 `SHA256SUMS`와 `shasum -a 256 <파일>`(macOS) 또는 `Get-FileHash <파일> -Algorithm SHA256`(Windows) 결과를 비교하세요.

### 시험 결과

실제 Chrome 종단 시험(E2E)이 현재 빌드에서 macOS·Windows 모두 **100% 통과**합니다.

### 자주 묻는 질문

- **평소 쓰는 Chrome은 안전한가요?** 네. wwt-lite는 따로 만든 전용 프로필로 Chrome을 띄웁니다. 평소 프로필의 쿠키·기록·저장된 비밀번호는 읽지도 바꾸지도 않고, 평소 Chrome과 나란히 써도 됩니다.
- **비밀번호는요?** 비밀번호·쿠키·토큰을 읽거나 저장하거나 보내지 않습니다. 로그인이 필요하면 에이전트가 창을 넘겨주고 내가 직접 입력합니다. `wwt-browser setup`으로 미리 한 번 로그인해 둘 수도 있고, 그 로그인은 내 컴퓨터의 wwt-lite 전용 프로필에만 남습니다.
- **무료인가요?** 네. [라이선스](LICENSE.md)상 개인·업무용 모두 무료로 쓸 수 있습니다.
- **Windows에서 SmartScreen 경고가 떠요.** Windows 빌드는 아직 코드 서명이 없어서 "알 수 없는 게시자" 경고가 뜰 수 있습니다. 설치기가 모든 파일을 `SHA256SUMS`와 대조하고, 직접 검증할 수도 있습니다.
- **Intel Mac, Linux는요?** 아직 지원하지 않습니다. 베타는 Apple 칩 Mac(macOS 13.5+)과 Windows 10/11 x64만 지원합니다. 필요하면 이슈로 알려 주세요.
- **내 데이터가 어디로 가나요?** 사용 정보 수집이 없습니다. 페이지·스크린샷·로그는 내 컴퓨터에 남고, 내가 돌리는 에이전트에게만 전달됩니다.

### 라이선스·보안·개인정보

[LICENSE.md](LICENSE.md)(무료 사용, 수정·역분석·재배포 금지), [SECURITY.md](SECURITY.md)(취약점은 Security 탭의 Report a vulnerability로), [PRIVACY.md](PRIVACY.md)(사용 정보 수집 없음).
