# wwt-lite

wwt-lite is a browser for AI agents. Claude Code, Codex and other coding agents drive a real Chrome window through it, while you can watch and take over at any time.

This repository only hosts release downloads (installers, one-line install scripts and checksums). Source code is not published here.

> **Status:** public beta — [v0.1.0-beta.1](https://github.com/d2wolab/wwt-lite-releases/releases/tag/v0.1.0-beta.1). Expect changes; please report issues.

[한국어 안내는 아래에 있습니다.](#한국어)

## Requirements

- macOS 13.5 or later (Apple silicon) or Windows 10/11 (x64)
- Google Chrome installed
- No separate Node.js install needed (it is bundled)

## Install

macOS:

```bash
curl -fsSL https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.sh | sh
```

Windows (PowerShell):

```powershell
irm https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.ps1 | iex
```

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

## License, security and privacy

- [License (EULA)](LICENSE.md): free to use; no modification, reverse engineering or redistribution.
- [Security](SECURITY.md): what wwt-lite does and does not do, and how to report a vulnerability.
- [Privacy](PRIVACY.md): no telemetry; everything stays on your computer.

---

## 한국어

wwt-lite는 AI 에이전트용 브라우저입니다. Claude Code, Codex 같은 에이전트가 실제 Chrome 창을 조작하고, 사람은 지켜보다가 언제든 직접 잡을 수 있습니다. 이 저장소에는 설치 파일과 설치 스크립트만 있고 소스 코드는 없습니다.

> **상태:** 공개 베타 [v0.1.0-beta.1](https://github.com/d2wolab/wwt-lite-releases/releases/tag/v0.1.0-beta.1). 바뀔 수 있으니 문제가 있으면 이슈로 알려 주세요.

**필요한 것:** macOS 13.5 이상(Apple 칩) 또는 Windows 10/11(x64), Google Chrome. Node.js는 함께 들어 있어 따로 설치하지 않아도 됩니다.

**설치**

macOS:

```bash
curl -fsSL https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.sh | sh
```

Windows (PowerShell):

```powershell
irm https://github.com/d2wolab/wwt-lite-releases/releases/latest/download/install.ps1 | iex
```

설치기는 받은 파일의 SHA-256 지문을 `SHA256SUMS`와 비교한 뒤, 관리자 권한 없이 내 사용자 폴더에 설치합니다. `wwt-browser` 명령, 엔진, 메뉴 막대(트레이) 앱, 에이전트용 `wwt-browser` 스킬이 함께 설치됩니다. 메뉴 막대 앱이 필요 없으면 `--no-menubar`를 붙이세요.

macOS 빌드는 Apple Developer ID로 서명하고 공증합니다. Windows 빌드는 아직 코드 서명이 없습니다.

**Claude Code, Codex에서 쓰기:** 설치하면 스킬이 자동으로 등록됩니다. "wwt-browser로 example.com 열어서 요약해 줘"처럼 요청하면 됩니다. 에이전트가 작업하는 동안 창 아래 제어 막대에서 **Take over**(직접 하기), **Resume**(다시 맡기기), 정지 아이콘(작업 끝내기)을 쓸 수 있습니다.

**업데이트:** 설치 명령을 다시 실행하거나 `wwt-browser upgrade`.

**엔진 끄기:** 엔진은 에이전트가 쓸 때 자동으로 켜집니다. 끄려면 메뉴 막대(트레이) 앱의 **⋯ → 종료**, 멈춘 것 같으면 **엔진 다시 시작**.

**삭제:** 위 영어 안내의 Uninstall 명령을 실행하세요. 평소 쓰는 Chrome 프로필은 건드리지 않습니다.

**라이선스·보안·개인정보:** [LICENSE.md](LICENSE.md)(무료 사용, 수정·역분석·재배포 금지), [SECURITY.md](SECURITY.md), [PRIVACY.md](PRIVACY.md)(사용 정보 수집 없음).
