---
id: powershell-commands
title: "3. 자주 사용하는 PowerShell 기본 명령어"
sidebar_position: 3
description: 실습 중 자주 쓰게 될 PowerShell 명령어를 미리 정리했습니다
---

# PowerShell 기본 명령어

> 이 문서는 [Node.js 설치](./nodejs-install)를 마친 뒤, 본격적인 실습([Section 1. Git 기초](/curriculum/git-basics))에 들어가기 전 참고용으로 보시면 됩니다. 외우실 필요는 없고, 실습 중 막히면 다시 돌아와 찾아보세요.

## 위치 확인 & 이동

| 명령어 | 설명 |
|---|---|
| `pwd` | 지금 내가 있는 폴더 위치 확인 (`Get-Location`) |
| `ls` | 현재 폴더 안 파일·폴더 목록 보기 (`Get-ChildItem`) |
| `cd 폴더명` | 해당 폴더로 이동 (`Set-Location`) |
| `cd ..` | 한 단계 상위 폴더로 이동 |
| `cd ~` | 사용자 홈 폴더(`C:\Users\사용자명`)로 이동 |
| `cd \` | 드라이브 최상위(`C:\`)로 이동 |

```powershell
PS C:\Users\you> cd Desktop
PS C:\Users\you\Desktop> ls

    Directory: C:\Users\you\Desktop

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         2026-07-01   10:23                my-project
```

## 파일 · 폴더 만들기 / 지우기

| 명령어 | 설명 |
|---|---|
| `mkdir 폴더명` | 새 폴더 만들기 |
| `New-Item 파일명.txt` | 새 빈 파일 만들기 |
| `rm 파일명` | 파일 삭제 |
| `rm -r 폴더명` | 폴더 전체 삭제 (하위 파일 포함) |
| `cp 원본 대상` | 파일 복사 |
| `mv 원본 대상` | 파일 이동 / 이름 변경 |

:::caution[삭제는 되돌릴 수 없습니다]
PowerShell에서 `rm`으로 지운 파일은 휴지통을 거치지 않고 바로 삭제되는 경우가 많습니다. 지우기 전에 한 번 더 확인하는 습관을 들이세요.
:::

## 파일 내용 확인

| 명령어 | 설명 |
|---|---|
| `cat 파일명` | 파일 내용을 화면에 출력 (`Get-Content`) |
| `code 파일명` | VS Code로 파일 열기 (VS Code 설치 & PATH 등록 시) |
| `notepad 파일명` | 메모장으로 파일 열기 |

```powershell
PS C:\Users\you\my-project> cat Code.gs
function cleanUp() {
  // ...
}
```

## 화면 정리 & 종료

| 명령어 | 설명 |
|---|---|
| `cls` | 터미널 화면 지우기 (`clear`와 동일하게 동작) |
| `exit` | 터미널 창 닫기 |

## 편하게 쓰는 단축키

| 단축키 | 설명 |
|---|---|
| `Tab` | 폴더/파일 이름을 끝까지 안 쳐도 자동완성 |
| `↑` / `↓` | 이전에 입력했던 명령어를 순서대로 다시 불러오기 |
| `Ctrl + C` | 실행 중인 작업을 강제로 멈추기 |
| `Ctrl + L` | 화면 지우기 (`cls`와 동일) |

:::tip[명령어가 기억 안 나면]
`Get-Help 명령어이름` 을 입력하면 PowerShell이 해당 명령어의 사용법을 보여줍니다. 예: `Get-Help Get-ChildItem`
:::

## 자주 헷갈리는 부분

- **`ls`, `cat`, `cls` 는 사실 PowerShell의 진짜 명령어(cmdlet)가 아니라, `Get-ChildItem`·`Get-Content`·`Clear-Host` 같은 cmdlet에 연결된 "별칭(alias)"입니다. 리눅스/macOS 사용자에게 익숙하도록 미리 연결해둔 것이라, 편하게 그대로 쓰시면 됩니다.
- **Git 명령어(`git status`, `git add` 등)는 PowerShell 명령어가 아니라 Git 프로그램의 명령어**입니다. Git이 설치되어 있어야 동작하며, 이 문서의 명령어들과는 별개입니다. Git 명령어는 [Section 1. Git 기초](/curriculum/git-basics)에서 자세히 다룹니다.

---

**다음:** [Section 1. Git 기초 개념 & 설치 & 실습](/curriculum/git-basics)
