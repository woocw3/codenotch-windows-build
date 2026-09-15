# Codenotch — Codex·Claude 사용량 한눈에 보기 / See Codex & Claude usage at a glance (Windows)

[한국어](#한국어-안내) · [English](#english-guide)

## 한국어 안내

Codenotch는 화면 오른쪽 위젯에서 **Codex와 Claude Code의 사용량을 바로 확인**할 수 있는 Windows 프로그램입니다. 각 서비스에 로그인하면 남은 사용량과 갱신 시점을 한 화면에서 볼 수 있습니다.

이 저장소는 [원본 Codenotch](https://github.com/vinzdg/codenotch)의 Windows 64비트용 비공식 빌드(v0.3.0)를 배포합니다. 원본 커밋은 [`6c28672c300fadcb7fb59a277ba9d3997d74f1d2`](https://github.com/vinzdg/codenotch/commit/6c28672c300fadcb7fb59a277ba9d3997d74f1d2)이며, 원본의 MIT 라이선스는 [LICENSE](LICENSE)에 포함했습니다.

## 다른 Windows PC에 설치하기

1. **[설치 프로그램 다운로드](https://raw.githubusercontent.com/woocw3/codenotch-windows-build/main/downloads/Codenotch-Windows-v0.3.0-Setup-x64.exe)**를 눌러 `Codenotch-Windows-v0.3.0-Setup-x64.exe`를 저장합니다.
2. 다운로드한 `.exe` 파일을 더블클릭하고 설치 마법사의 안내를 따릅니다. 시작 메뉴에 Codenotch 바로가기가 생기며, 설치 과정에서 바탕화면 바로가기도 선택할 수 있습니다.
3. 화면 오른쪽에 Codenotch 위젯이 나타나는지 확인합니다. 다음에 실행할 때는 시작 메뉴의 **Codenotch**를 선택합니다. 검색에 나오지 않으면 `Win + R`을 눌러 `%LOCALAPPDATA%\Programs\Codenotch\codenotch.exe`를 입력합니다.

[ZIP 파일](https://github.com/woocw3/codenotch-windows-build/releases/download/v0.3.0-windows/Codenotch-Windows-v0.3.0-x64.zip)에도 설치 프로그램이 들어 있습니다. 설치 없이 사용하려면 ZIP을 풀고 `codenotch.exe`를 실행하세요. 이때 `codenotch-hook.exe`는 같은 폴더에 두세요.

## 사용량이 표시되지 않을 때

사용량은 **설치한 PC의 로그인 정보**를 읽습니다. 그 PC에서 Codex에 로그인하고, Claude 사용량을 보려면 Claude Code를 설치해 아래 명령으로 로그인하세요.

```powershell
claude auth login --claudeai
```

로그인을 마친 뒤 Codenotch를 종료하고 다시 실행하세요. 실행 시 WebView2가 필요하다는 메시지가 나오면 Microsoft Edge WebView2 Runtime을 설치하세요.

## Codex(GPT)는 바로 보이는데 Claude만 늦게 보일 때

두 사용량은 읽는 방법이 다릅니다.

- **Codex**는 PC에 남아 있는 세션 기록(`~/.codex/sessions/...`의 rollout 로그)을 바로 읽을 수 있어, 네트워크 요청이 실패해도 마지막 값이 즉시 나옵니다.
- **Claude**는 로컬 기록이 없습니다. `%USERPROFILE%\.claude\.credentials.json`의 토큰으로 Anthropic 사용량 API를 호출해야만 값이 생기고, 조회 주기는 1분(사용 중)~5분(유휴)입니다. 그래서 실행 직후에는 비어 있을 수 있습니다.

확인 순서는 다음과 같습니다.

1. **토큰 파일이 있는지 확인**합니다. `%USERPROFILE%\.claude\.credentials.json`이 없으면 Claude 칸은 계속 로그인 필요 상태입니다. 이 파일은 **독립 실행형 Claude Code CLI**만 만듭니다. Claude 데스크톱 앱(또는 앱에 내장된 Claude Code)으로 로그인하면 토큰이 앱 전용 저장소에 들어가 Codenotch가 읽지 못합니다. 터미널에서 `claude auth status`로 로그인 상태를 확인하세요.
2. **토큰을 갱신**합니다. 토큰은 발급 후 약 8시간이면 만료되고, 만료된 토큰은 CLI를 한 번 실행해야 새로 발급됩니다. 터미널에서 `claude`를 한 번 실행했다가 종료한 뒤, 트레이 아이콘 메뉴에서 **사용량 지금 새로고침**을 누르세요.
3. **바로 갱신되지 않으면 잠시 기다립니다.** 배포된 v0.3.0 빌드는 만료된 토큰을 그대로 보내고, 서버는 여기에 429와 함께 약 1시간짜리 Retry-After를 돌려줍니다. 그러면 Codenotch는 그 시간만큼 조회를 멈추므로, 2번을 먼저 하고(토큰을 유효하게 만든 뒤) 새로고침하는 것이 가장 빠릅니다. Codenotch를 껐다 켜도 대기 시간은 저장되어 유지됩니다.
4. **진단 로그를 봅니다.** 명령 프롬프트에서 `%LOCALAPPDATA%\Programs\Codenotch\codenotch.exe doctor`를 실행하면 자격증명 탐지 결과가 출력되고 `%APPDATA%\codenotch\doctor.log`에도 저장됩니다.

만료 토큰을 자동으로 갱신하는 수정(원본 커밋 [`27e4b34`](https://github.com/vinzdg/codenotch/commit/27e4b34))은 이 빌드가 기준으로 삼은 커밋 이후에 원본에 들어갔습니다. 즉 위 2번 과정은 이 빌드에서만 필요한 수동 작업입니다.

이 설치 프로그램은 전자서명이 없어 Windows에서 게시자 경고가 표시될 수 있습니다. 패키지에 계정 인증정보나 개인 설정은 포함하지 않았습니다.

## 파일 확인용 SHA-256

- 설치 프로그램: `DBBE6A6B3329A332EF5C037CF88FD8C08B86A071843F7344505F9005259156F3`
- ZIP: `8E88BEA9EE63E0EA8BE9E77B8B2073EBE5D91C460314840EAD912F8BFBA0B9DC`

---

## English guide

Codenotch is a Windows widget that lets you **check Codex and Claude Code usage at a glance**. After signing in to each service on your PC, you can see usage and reset times together in the widget on the right edge of the screen.

This repository distributes an unofficial Windows x64 build of [vinzdg/codenotch](https://github.com/vinzdg/codenotch), v0.3.0, built from upstream commit [`6c28672c300fadcb7fb59a277ba9d3997d74f1d2`](https://github.com/vinzdg/codenotch/commit/6c28672c300fadcb7fb59a277ba9d3997d74f1d2). The original project is MIT-licensed; see [LICENSE](LICENSE).

### Install on another Windows PC

1. [Download the Setup executable](https://raw.githubusercontent.com/woocw3/codenotch-windows-build/main/downloads/Codenotch-Windows-v0.3.0-Setup-x64.exe). Save `Codenotch-Windows-v0.3.0-Setup-x64.exe`.
2. Double-click the downloaded file and follow the setup wizard. It creates a Start Menu shortcut and offers an optional desktop shortcut.
3. Check that the widget appears on the right edge of the screen. To start it again, select **Codenotch** from the Start Menu. If search does not find it, press `Win + R` and enter `%LOCALAPPDATA%\Programs\Codenotch\codenotch.exe`.

The [ZIP archive](https://github.com/woocw3/codenotch-windows-build/releases/download/v0.3.0-windows/Codenotch-Windows-v0.3.0-x64.zip) also contains the Setup executable and portable binaries. For portable use, extract the ZIP and run `codenotch.exe` with `codenotch-hook.exe` in the same folder.

### If usage is missing

Usage is read from sign-ins **on the PC where you install Codenotch**. Sign in to Codex on that PC. To show Claude usage, install Claude Code and sign in with:

```powershell
claude auth login --claudeai
```

Restart Codenotch after signing in. If Windows asks for WebView2, install Microsoft Edge WebView2 Runtime.

### If Codex (GPT) shows up right away but Claude does not

The two readings come from different places.

- **Codex** can read session history left on the PC (the rollout logs under `~/.codex/sessions/...`), so the last known number appears instantly even when a network call fails.
- **Claude** has no local history. A number exists only after Codenotch calls the Anthropic usage API with the token in `%USERPROFILE%\.claude\.credentials.json`, and it polls every 1 minute while you work, every 5 minutes when idle. So the cell can be empty right after startup.

Work through this:

1. **Check that the token file exists.** Without `%USERPROFILE%\.claude\.credentials.json` the Claude cell stays in the "needs sign-in" state. Only the **standalone Claude Code CLI** writes that file. Signing in through the Claude desktop app (or the Claude Code bundled inside it) stores the token in the app's own store, which Codenotch cannot read. Run `claude auth status` in a terminal to check.
2. **Refresh the token.** The token expires roughly 8 hours after it is issued, and only a run of the CLI issues a new one. Start `claude` once in a terminal, exit it, then pick **Refresh usage now** from the tray icon menu.
3. **If it still does not update, wait it out.** The published v0.3.0 build sends an expired token as-is, and the server answers with 429 plus a Retry-After of about an hour, during which Codenotch makes no further calls. Doing step 2 first (so the token is valid) and then refreshing is the fastest path. The wait is persisted, so restarting Codenotch does not clear it.
4. **Read the diagnostics.** Run `%LOCALAPPDATA%\Programs\Codenotch\codenotch.exe doctor` from a command prompt; it prints what it found for the credential and also writes `%APPDATA%\codenotch\doctor.log`.

The upstream fix that renews an expired token automatically (commit [`27e4b34`](https://github.com/vinzdg/codenotch/commit/27e4b34)) landed after the commit this build was made from, so step 2 is a manual workaround specific to this build.

This installer is unsigned, so Windows may display an unknown publisher warning. The package contains no account credentials or personal settings.

### SHA-256

- Setup EXE: `DBBE6A6B3329A332EF5C037CF88FD8C08B86A071843F7344505F9005259156F3`
- ZIP: `8E88BEA9EE63E0EA8BE9E77B8B2073EBE5D91C460314840EAD912F8BFBA0B9DC`
