---
id: github-pat
title: "GitHub 개인 액세스 토큰(PAT) 생성"
sidebar_position: 4
description: git push 시 필요한 GitHub 개인 액세스 토큰(Personal Access Token) 발급 방법
---

# GitHub 개인 액세스 토큰(PAT) 생성

> GitHub는 보안상의 이유로 비밀번호를 이용한 Git 인증을 더 이상 지원하지 않습니다. `git push`처럼 GitHub 저장소에 접속해야 하는 작업에는 비밀번호 대신 **개인 액세스 토큰(Personal Access Token, PAT)** 을 사용합니다.

## PAT가 왜 필요한가

HTTPS 방식으로 GitHub 저장소에 연결하면(`https://github.com/...`), `git push` 실행 시 사용자명과 비밀번호를 물어보는 로그인 창이 뜹니다. 이때 비밀번호 칸에 실제 GitHub 비밀번호를 입력하면 인증에 실패합니다. **비밀번호 대신 PAT을 붙여넣어야** 정상적으로 인증됩니다.

:::note[SSH 방식도 있습니다]
SSH 키를 등록해 인증하는 방법도 있지만, 오늘 실습은 별도 키 관리가 필요 없는 HTTPS + PAT 방식을 기준으로 안내합니다.
:::

## 1단계 — 토큰 발급 페이지로 이동

1. GitHub 로그인 후 우측 상단 프로필 아이콘 클릭 → **Settings**
2. 좌측 메뉴 맨 아래 **Developer settings** 클릭
3. **Personal access tokens** → **Tokens (classic)** 선택
4. **Generate new token** → **Generate new token (classic)** 클릭

:::tip
Fine-grained tokens(저장소별 세밀한 권한 설정)도 있지만, 처음 설정하는 경우 범위를 이해하기 쉬운 **Tokens (classic)** 으로 시작하는 것을 권장합니다.
:::

## 2단계 — 토큰 설정

| 항목 | 설정값 |
|---|---|
| Note | 토큰의 용도를 알아볼 수 있는 이름 (예: `hyu-vibe-coding-laptop`) |
| Expiration | 만료 기간 (예: 90 days) — 기간이 지나면 토큰이 자동 만료되어 재발급 필요 |
| Select scopes | 최소한 **`repo`** 체크박스 선택 (private/public 저장소 push·pull에 필요) |

:::caution[만료 기간을 짧게 두는 이유]
토큰은 사실상 비밀번호와 같은 권한을 가지므로, 유출 위험을 줄이기 위해 필요 이상으로 긴 만료 기간은 피하는 것이 안전합니다. 만료되면 이 페이지에서 새로 발급하면 됩니다.
:::

페이지 맨 아래 **Generate token** 버튼을 클릭합니다.

## 3단계 — 토큰 복사 & 보관

생성 직후 화면에 초록색 배경으로 토큰 문자열(`ghp_`로 시작)이 **단 한 번만** 표시됩니다.

:::danger[지금 복사하지 않으면 다시 볼 수 없습니다]
이 화면을 벗어나면 토큰 전체 문자열을 다시 확인할 수 없습니다. 반드시 지금 복사해서 비밀번호 관리자 등 안전한 곳에 보관하세요. 토큰을 잃어버리면 기존 토큰은 삭제하고 새로 발급해야 합니다.
:::

## 4단계 — git push에서 사용하기

```powershell
git push -u origin main
# Username for 'https://github.com': 여기에 GitHub 아이디 입력
# Password for 'https://...': 여기에 GitHub 비밀번호가 아니라 방금 복사한 PAT을 붙여넣기
```

:::tip[매번 입력하기 번거롭다면]
Git for Windows에는 **Git Credential Manager**가 기본 포함되어 있어, 최초 1회 PAT을 입력하면 이후에는 인증 정보를 안전하게 기억해 다시 묻지 않습니다. 별도 설정이 필요하지 않습니다.
:::

## 트러블슈팅

| 증상 | 원인 / 해결 |
|---|---|
| `remote: Support for password authentication was removed` | 비밀번호 칸에 GitHub 비밀번호를 입력한 경우. 발급받은 PAT을 대신 입력 |
| `remote: Permission to ... denied` / `403` | 토큰의 **Select scopes**에서 `repo` 체크가 안 되어 있었을 가능성. 토큰을 재발급하며 `repo` 범위 포함 |
| 예전에 저장된 잘못된 인증 정보가 계속 사용됨 | Windows **자격 증명 관리자**(제어판 → 사용자 계정 → Windows 자격 증명)에서 `git:https://github.com` 항목을 삭제 후 다시 push하며 새 PAT 입력 |
| 토큰이 만료되어 push 실패 | 1~3단계를 반복해 새 토큰을 발급하고, 다음 push 시 새 토큰으로 재인증 |

---

**다음:** [Node.js 최신 LTS 설치](./nodejs-install)
