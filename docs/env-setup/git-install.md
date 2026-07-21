---
id: git-install
title: "Git 설치 & 최초 설정"
sidebar_position: 3
description: 실습에 필요한 Git 설치 방법과 최초 1회 설정
---

# Git 설치 & 최초 설정

> 이 단계는 [PowerShell 기본 명령어](./powershell-commands)를 확인한 뒤 진행합니다. **PowerShell 7** 창에서 실행하세요.

## 0단계 — 이미 설치되어 있는지 확인

```powershell
git --version
# git version 2.43.0
```

버전이 출력되면 [3단계 최초 설정](#3단계--최초-1회-설정-사용자-정보)만 확인하고 넘어가시면 됩니다. `'git'은(는) 내부 또는 외부 명령... 인식되지 않습니다`라는 오류가 나오면 아래 단계를 진행하세요.

## 1단계 — 설치

### 방법 A. winget으로 설치 (권장)

```powershell
winget install --id Git.Git -e --source winget
```

설치 가능한 버전 목록은 아래 명령어로 확인할 수 있습니다.

```powershell
winget show --id Git.Git --versions
```

### 방법 B. 공식 설치 파일 직접 다운로드

사내 방화벽 등으로 winget 사용이 어려운 경우 사용합니다.

1. [git-scm.com](https://git-scm.com/download/win) 접속
2. **64-bit Git for Windows Setup** 다운로드
3. 설치 파일 실행 → 설치 마법사에서 기본값으로 "Next" 진행

:::tip
설치 마법사 중간에 "Choosing the default editor used by Git" 같은 화면이 나오는데, 오늘 실습에서는 기본값(또는 익숙한 에디터)을 그대로 두고 넘어가셔도 무방합니다.
:::

## 2단계 — 설치 확인

설치 후 **기존에 열려 있던 터미널 창은 모두 닫고**, PowerShell 7을 새로 실행합니다.

```powershell
git --version
# git version 2.43.0
```

## 3단계 — 최초 1회 설정 (사용자 정보)

Git으로 커밋을 남기려면, "누가 커밋했는지" 이름과 이메일을 먼저 등록해야 합니다. 이 PC에서 처음 Git을 쓰는 경우 한 번만 해두면 됩니다.

```powershell
git config --global user.name "홍길동"
git config --global user.email "you@hanyang.ac.kr"
```

등록된 값 확인:

```powershell
git config --global --list
# user.name=홍길동
# user.email=you@hanyang.ac.kr
```

:::note[이메일은 왜 등록하나요?]
나중에 GitHub 계정과 연결할 때, 여기 등록한 이메일이 커밋 작성자를 식별하는 데 쓰입니다. 가능하면 실제 사용하시는 GitHub 계정의 이메일과 동일하게 맞춰두는 것을 권장합니다.
:::

## 트러블슈팅

| 증상 | 원인 / 해결 |
|---|---|
| 설치 후에도 `git` 인식 안 됨 | 터미널이 PATH 변경을 반영 못한 상태. 터미널 완전 종료 후 재실행 (필요시 PC 재부팅) |
| `git commit` 시 "Please tell me who you are" 오류 | 3단계의 `user.name` / `user.email` 설정이 안 된 상태. 위 명령어로 설정 후 재시도 |
| 회사 프록시 환경에서 clone/push 실패 | `git config --global http.proxy http://프록시주소:포트` 설정 필요 (담당 IT팀에 프록시 주소 확인) |

---

**다음:** [GitHub 개인 액세스 토큰(PAT) 생성](./github-pat)
