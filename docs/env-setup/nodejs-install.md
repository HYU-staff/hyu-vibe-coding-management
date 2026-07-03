---
id: nodejs-install
title: "2. PowerShell에서 Node.js 최신 LTS 설치"
sidebar_position: 2
description: AI CLI 도구와 clasp 실행에 필요한 Node.js LTS 설치 방법
---

# PowerShell에서 Node.js 최신 LTS 설치

> 이 단계는 [PowerShell 7 설치](./powershell-install)를 마친 뒤 진행합니다. AI CLI 도구, `clasp` 등 오늘 사용할 도구들은 모두 Node.js 위에서 동작합니다.

## LTS란?

**LTS(Long Term Support)**는 Node.js 버전 중 "가장 안정적으로 장기 지원되는 버전"을 뜻합니다. 최신 기능이 가장 많은 버전(Current)이 아니라, 오류가 적고 오래 유지보수되는 버전을 선택하는 것이 실무에서는 안전합니다. 오늘 실습은 LTS 버전을 기준으로 합니다.

## 0단계 — 이미 설치되어 있는지 확인

**PowerShell 7** 창에서 아래 명령어를 실행합니다.

```powershell
node -v
npm -v
```

버전이 출력되면 [설치 확인](#3단계--설치-확인) 단계에서 LTS 버전인지만 확인하면 됩니다. 명령어를 찾을 수 없다는 오류가 나오면 아래 단계를 진행하세요.

:::caution
반드시 **PowerShell 7 (검은 아이콘)** 창에서 실행하세요. Windows PowerShell 5.1에서도 동작은 하지만, 오늘 실습 환경과 PATH 설정을 통일하기 위해 PowerShell 7을 기준으로 안내합니다.
:::

## 1단계 — 설치

### 방법 A. winget으로 설치 (권장)

```powershell
winget install OpenJS.NodeJS.LTS
```

특정 메이저 버전을 고정하고 싶다면 버전을 지정할 수 있습니다.

```powershell
# 설치 가능한 버전 목록 확인
winget show --id OpenJS.NodeJS.LTS --versions

# 특정 버전 설치
winget install --id OpenJS.NodeJS.LTS --version 22.14.0
```

### 방법 B. 공식 설치 파일 직접 다운로드

사내 방화벽 등으로 winget이 어려운 경우:

1. [nodejs.org](https://nodejs.org) 접속
2. **"LTS"** 라벨이 붙은 버전의 Windows Installer(.msi) 다운로드 (64비트 PC 기준 `node-v22.x.x-x64.msi`)
3. 설치 파일 실행 → 설치 마법사에서 기본값으로 진행
   - **"Automatically install the necessary tools"** 체크박스는 선택하지 않아도 됩니다 (오늘 실습에는 불필요)

## 2단계 — 여러 버전을 관리해야 한다면 (선택, 심화)

팀마다 다른 Node.js 버전이 필요하거나, 프로젝트별로 버전을 바꿔가며 작업해야 한다면 **nvm-windows**를 사용하는 것이 편리합니다.

```powershell
# 1) 기존에 winget/설치파일로 설치한 Node.js가 있다면 먼저 제거
winget uninstall OpenJS.NodeJS.LTS

# 2) nvm-windows 설치
winget install CoreyButler.NVMforWindows

# 3) 새 PowerShell 창을 열고 최신 LTS 설치
nvm install lts

# 4) 설치된 버전 목록 확인
nvm list

# 5) 사용할 버전 활성화 (관리자 권한 PowerShell 필요)
nvm use 22.14.0
```

:::note
nvm-windows는 일반 nvm(macOS/Linux용)과 명령어 체계가 다릅니다. 오늘 처음 환경을 설정하는 것이라면 방법 A(winget 단일 설치)로 충분하며, nvm-windows는 나중에 여러 프로젝트를 동시에 다루게 될 때 도입해도 늦지 않습니다.
:::

## 3단계 — 설치 확인

설치 후 **열려 있던 PowerShell 창을 모두 닫고 새로 실행**합니다. (PATH 환경 변수는 새 터미널부터 적용됩니다.)

```powershell
node -v
# v22.14.0

npm -v
# 10.9.0
```

## 4단계 — npm 기본 설정 점검 (선택)

```powershell
# 전역 패키지가 설치되는 경로 확인
npm config get prefix

# 현재 PATH에 해당 경로가 포함되어 있는지 확인
$env:PATH -split ';' | Select-String 'npm'
```

전역 설치한 CLI 도구(`npm install -g ...`)를 실행했는데 명령어를 찾을 수 없다는 오류가 나면, 위 경로가 PATH에 없는 경우가 대부분입니다. 이 경우 새 터미널을 열거나 PC를 재부팅해 PATH를 다시 불러오세요.

## 트러블슈팅

| 증상 | 원인 / 해결 |
|---|---|
| 설치 후에도 `node` 인식 안 됨 | 터미널이 PATH 변경을 반영 못한 상태. 터미널 완전 종료 후 재실행 |
| `npm install -g` 로 설치한 도구가 실행 안 됨 | `npm config get prefix` 경로가 시스템 PATH에 없는지 확인 |
| 회사 프록시 환경에서 npm install 실패 | `npm config set proxy http://프록시주소:포트`, `npm config set https-proxy http://프록시주소:포트` 설정 필요 (담당 IT팀에 프록시 주소 확인) |
| nvm 사용 중 "권한이 없습니다" 오류 | PowerShell을 관리자 권한으로 실행 후 `nvm use` 재시도 |

---

**다음:** [Section 1. Git 기초 개념 & 설치 & 실습](/curriculum/git-basics)
