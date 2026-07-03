---
id: powershell-install
title: "1. Windows PowerShell 7.6.0 설치"
sidebar_position: 1
description: 최신 PowerShell 7을 설치하고 확인하는 방법
---

# Windows PowerShell 7.6.0 설치

> 이 문서는 로컬 PC 환경 설정의 첫 단계입니다. 모든 실습은 **PowerShell 7**(pwsh)을 기준으로 진행됩니다.

## 왜 PowerShell 7이 필요한가

Windows에는 기본적으로 "Windows PowerShell 5.1"이 내장되어 있지만, 이는 구버전이라 최신 기능과 크로스플랫폼 지원이 부족합니다. PowerShell 7은 별도로 설치해야 하는 최신 버전입니다.

| 구분 | Windows PowerShell (기본 내장) | PowerShell 7 (별도 설치) |
|---|---|---|
| 아이콘 색상 | 파란색 | 검은색 |
| 버전 | 5.1 고정 | 7.6.0 등 최신 버전 |
| 실행 파일 | `powershell.exe` | `pwsh.exe` |

:::caution[헷갈리지 마세요]
작업 표시줄이나 시작 메뉴에 두 아이콘이 함께 보일 수 있습니다. 오늘 실습은 반드시 **검은색 아이콘(PowerShell 7)**을 사용합니다.
:::

## 0단계 — 이미 설치되어 있는지 확인

먼저 기존 PowerShell 5.1을 열고 아래 명령어로 PowerShell 7이 이미 설치되어 있는지 확인합니다.

```powershell
pwsh -v
```

버전이 출력되면 [설치 확인](#3단계--설치-확인) 단계로 건너뛰어 버전이 7.6.0인지만 확인하세요. `'pwsh'은(는) 내부 또는 외부 명령... 인식되지 않습니다`라는 오류가 나오면 아직 설치되지 않은 것이므로 아래 단계를 진행합니다.

## 1단계 — 사전 요구사항

- Windows 10 (버전 1809 이상) 또는 Windows 11
- winget(앱 설치 관리자)이 기본 포함되어 있어야 함 — Windows 10 21H1 이상 / Windows 11은 기본 포함
- winget 설치 여부 확인:

```powershell
winget --version
```

오류가 나면 Microsoft Store에서 **"앱 설치 관리자(App Installer)"**를 검색해 설치한 뒤 다시 시도하세요.

## 2단계 — 설치

### 방법 A. winget으로 설치 (권장)

가장 간단하고 자동 업데이트 관리도 편한 방법입니다.

```powershell
# 특정 버전(7.6.0)을 지정해서 설치
winget install --id Microsoft.PowerShell --version 7.6.0 --source winget

# 버전을 지정하지 않으면 winget이 제공하는 최신 안정 버전이 설치됩니다
winget install --id Microsoft.PowerShell --source winget
```

설치 가능한 버전 목록은 아래 명령어로 확인할 수 있습니다.

```powershell
winget show --id Microsoft.PowerShell --versions
```

:::tip
사내 정책상 특정 버전(7.6.0)으로 통일해야 한다면 반드시 `--version` 옵션을 명시하세요. 옵션 없이 설치하면 시점에 따라 더 최신 버전이 설치될 수 있습니다.
:::

### 방법 B. 설치 파일(MSI) 직접 다운로드

사내 방화벽 등으로 winget 사용이 어려운 경우 사용합니다.

1. [PowerShell GitHub Releases 페이지](https://github.com/PowerShell/PowerShell/releases)로 이동
2. `v7.6.0` 태그의 Assets 목록에서 `PowerShell-7.6.0-win-x64.msi` 파일 다운로드
   - PC가 32비트라면 `win-x86.msi`, ARM64 기기라면 `win-arm64.msi` 선택
3. 다운로드한 `.msi` 파일 실행 → 설치 마법사에서 기본값으로 "Next" 진행 → "Install"
4. 설치 마법사 옵션 화면에서 아래 두 항목은 체크된 상태로 두는 것을 권장합니다:
   - **Add PowerShell to Path Environment Variable**
   - **Enable PowerShell remoting**

## 3단계 — 설치 확인

설치 후 **기존에 열려 있던 터미널 창은 모두 닫고**, 시작 메뉴에서 **"PowerShell 7"**을 새로 실행합니다.

```powershell
PS C:\Users\you> $PSVersionTable.PSVersion

Major  Minor  Patch
-----  -----  -----
7      6      0
```

`Major.Minor.Patch`가 `7.6.0`으로 표시되면 정상 설치된 것입니다.

## 4단계 — 스크립트 실행 정책 확인 (선택)

기본 보안 정책상 로컬에서 작성한 `.ps1` 스크립트 실행이 차단될 수 있습니다. AI CLI 도구나 npm 스크립트 실행 중 아래와 같은 오류가 나면 실행 정책을 조정합니다.

```powershell
# 현재 정책 확인
Get-ExecutionPolicy

# 현재 사용자 범위에서만 로컬 서명되지 않은 스크립트 허용 (권장 설정)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

:::note
`-Scope CurrentUser`로 지정하면 관리자 권한 없이도 실행할 수 있고, 다른 사용자 계정에는 영향을 주지 않습니다.
:::

## 트러블슈팅

| 증상 | 원인 / 해결 |
|---|---|
| 설치 후에도 `pwsh` 인식 안 됨 | 기존 터미널 창이 PATH 변경을 반영하지 못한 상태. 터미널을 완전히 종료 후 재실행 (필요시 PC 재부팅) |
| winget 설치 시 권한 오류 | PowerShell을 "관리자 권한으로 실행"한 뒤 다시 시도 |
| 버전이 7.6.0이 아닌 다른 버전으로 설치됨 | 기존 버전을 제거(`winget uninstall --id Microsoft.PowerShell`) 후 `--version 7.6.0`을 명시해 재설치 |

---

**다음:** [2. PowerShell에서 Node.js 최신 LTS 설치](./nodejs-install)
