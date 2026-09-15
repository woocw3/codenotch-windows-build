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

This installer is unsigned, so Windows may display an unknown publisher warning. The package contains no account credentials or personal settings.

### SHA-256

- Setup EXE: `DBBE6A6B3329A332EF5C037CF88FD8C08B86A071843F7344505F9005259156F3`
- ZIP: `8E88BEA9EE63E0EA8BE9E77B8B2073EBE5D91C460314840EAD912F8BFBA0B9DC`
