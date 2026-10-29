<p align="center">
  <img src="assets/lumipilot-icon.png" alt="LumiPilot" width="128">
</p>

# LumiPilot

[English](README.md) | **한국어**

LumiPilot은 코딩과 일상 작업을 돕는 Windows 데스크톱 AI 어시스턴트입니다. AI 프로바이더와 작업 폴더를 선택해 파일을 읽고 수정하고, 명령을 실행하고, 웹을 탐색할 수 있습니다. 도구 실행에 필요한 승인은 사용자가 정합니다.

> 이 저장소는 Windows 앱을 배포합니다. 앱 소스 코드는 여기에 공개되어 있지 않습니다.

## 화면 미리보기

### 코딩 세션

여러 대화를 나란히 열고 도구 작업을 살펴보며, 명령을 실행하기 전에 승인할 수 있습니다.

<p align="center">
  <img src="assets/coding-session.png" alt="세 개의 코딩 세션과 도구 작업 내역, 명령 승인 창" width="860">
</p>

### 루미와 AI 프로바이더

루미에게 알림과 일정을 물어보고, 캐릭터 세션에서 사용할 AI 프로바이더를 선택합니다.

<p align="center">
  <img src="assets/character-session.png" alt="루미와 다가오는 일정, 알림을 요청하는 대화" width="320">
  <img src="assets/provide.png" alt="캐릭터 세션의 AI 프로바이더 선택 화면" width="320">
</p>

### 내장 브라우저

대화 옆에서 웹 페이지를 열고, 웹 콘텐츠를 활용하는 작업을 요청할 수 있습니다.

<p align="center">
  <img src="assets/web.png" alt="패키지 비교 대화 옆에 npm 패키지 페이지를 연 화면" width="860">
</p>

## 다운로드

**[Releases](https://github.com/lumipilot/LumiPilot/releases/latest)** 에서 최신 설치 파일 또는 포터블 ZIP을 받습니다.

1. 아래 중 하나와 같은 이름의 `.sha256` 파일을 받습니다.
   - 설치 파일: `LumiPilot-<버전>-build<N>-windows-x64-setup.exe`
   - 포터블 ZIP: `LumiPilot-<버전>-build<N>-windows-x64.zip`
2. 다운로드 폴더에서 PowerShell을 열고, 예시 이름을 실제 파일명으로 바꾼 뒤 두 해시를 비교합니다.
   ```powershell
   $File = 'LumiPilot-1.0.23-build123-windows-x64-setup.exe'
   (Get-FileHash -LiteralPath $File -Algorithm SHA256).Hash
   Get-Content -LiteralPath "$File.sha256"
   ```
   SHA-256 해시가 같아야 합니다. `build123`은 예시이며 실제 빌드 번호가 아닙니다.
3. 설치 파일을 실행하거나, ZIP을 원하는 곳에 풀고 `LumiPilot.exe`를 실행합니다.

설치 파일은 관리자 권한이 필요 없습니다. 현재 사용자에게만 설치하고 시작 메뉴 항목을 추가하며, Windows 설정 → 앱에서 제거할 수 있습니다. 제거해도 데이터와 설정(`%APPDATA%\LumiPilot`)은 지워지지 않습니다.

요구 사항: Windows 10/11(64비트). 브라우저 기능에는 Microsoft Edge WebView2 런타임이 필요합니다.

배포본에 코드 서명이 없다면 처음 실행할 때 Windows SmartScreen 경고가 뜰 수 있습니다. 체크섬은 다운로드 무결성을 확인하며 게시자의 신원을 보증하지는 않습니다.

선택 — Visual Studio 실시간 디버깅: Visual Studio를 닫고, 압축을 푼 폴더의 `extras\LumiPilotDebugBridge.vsix`를 실행한 뒤(Visual Studio 2022·2026) Visual Studio를 다시 엽니다. 확장에 서명이 없어 VSIX 설치 창이 경고할 수 있습니다. 크래시 덤프 분석은 이 확장 없이도 됩니다.

## 사용 설명서

처음이라면 **[사용 설명서](docs/user-guide.ko.md)** 에서 설정, 대화, 승인, 설정 항목, 문제 해결을 확인하세요.

## 할 수 있는 일

- **코딩 에이전트** — 작업 폴더의 파일을 읽고 검색하고 수정하며, 셸 명령을 실행하고, Git을 다루고, 파일 변경을 diff로 보여 줍니다.
- **여러 AI 프로바이더** — Anthropic, OpenAI, Google Gemini, xAI, NVIDIA, Z.ai, OpenRouter, OpenCode, Ollama(로컬), 그리고 직접 추가하는 OpenAI 호환 엔드포인트. 일부 프로바이더는 구독 계정 로그인도 지원하며, 허용 여부는 각 프로바이더의 약관을 따릅니다.
- **권한 제어** — 일반·편집 자동·전체 자동 모드, 도구별 허용/확인/거부 규칙, 계획 후 승인 흐름.
- **체크포인트** — 앱이 수정한 파일을 이전 턴 상태로 되돌립니다. 체크포인트는 별도 백업을 대체하지 않습니다.
- **서브에이전트·스킬·플러그인·MCP** — 서브에이전트에 작업을 위임하고, 스킬과 플러그인으로 기능을 늘리고, MCP 서버를 연결합니다.
- **내장 브라우저** — 웹 페이지, HTML 미리보기, 웹 자동화를 앱 안에서 처리합니다. 로그인 정보는 앱 전용 브라우저 프로필에만 남습니다.
- **연동** — Gmail·Google 캘린더·Drive(본인의 Google OAuth 클라이언트 필요), IMAP/SMTP 메일, 예약 작업.
- **음성·이미지** — 음성 입력과 음성 응답, 설정한 프로바이더를 통한 이미지 생성.
- **루미** — 작업 옆에서 함께하는 앱의 캐릭터입니다.

## 꼭 알아 두세요

- **샌드박스가 아닙니다.** 승인한 명령과 도구는 사용자 계정 권한 그대로 실행됩니다. 관리자 권한으로 실행하지 말고, 위험한 작업은 사본에서 먼저 해 보세요.
- **데이터는 사용자가 보낸 곳으로 갑니다.** 대화·파일·도구 결과는 선택한 AI 프로바이더와 연동 서비스로 전송됩니다. 앱은 사용 통계·대화·크래시 데이터를 개발자에게 보내지 않으며 업데이트 확인도 하지 않습니다.
- **비용.** 앱은 무료이지만 외부 AI 구독·API에는 비용이 들 수 있습니다.
- **AI는 틀릴 수 있습니다.** 변경 내용을 검토한 뒤 사용하세요.

데이터 위치: `%APPDATA%\LumiPilot\LumiPilot`

## 법적 고지

| 문서 | English | 한국어 |
|------|---------|--------|
| 무료 바이너리 라이선스 | [license](legal/en/license.txt) | [라이선스](legal/ko/license.txt) |
| 사용·안전 안내 | [usage](legal/en/usage.txt) | [사용·안전 안내](legal/ko/usage.txt) |
| 데이터 처리 안내 | [data](legal/en/data.txt) | [데이터 처리 안내](legal/ko/data.txt) |

같은 안내문은 앱을 처음 실행할 때에도 표시됩니다.

## 커뮤니티

사용 질문, 공개 버그 제보, 기능 제안은 [LumiPilot 공식 Discord](https://discord.gg/e3j5EnK3J)에서 받습니다. 한국어와 영어를 사용할 수 있습니다.

비공개 문의나 보안 관련 문제는 Discord가 아니라 메일로 보내 주세요.

## 문의

질문과 문제 신고: **lumipilothelp@gmail.com**

버전, 시각, 권한 모드, 증상, 재현 절차를 함께 적어 주세요. API 키, 비밀번호, 대화 전체, 저장소 전체는 보내지 마세요. 답변 기한은 약속하지 않습니다.
