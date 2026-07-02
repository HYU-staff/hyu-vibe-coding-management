---
id: github
title: "Section 2. GitHub 개념 & 사용법"
sidebar_position: 3
description: 내 코드를 클라우드에 안전하게 · 1시간
---

# Section 2. GitHub 개념 & 사용법

> 내 코드를 클라우드에 안전하게 · 1시간

## 로컬 백업만으로는 부족한 이유

- **기기 분실 / 고장** — 노트북이 고장 나면 로컬에만 있던 코드도 함께 사라집니다
- **실수로 삭제** — 실수로 파일이나 폴더 전체를 지워버릴 수 있습니다
- **다른 컴퓨터에서 이어하기** — 다른 자리, 다른 PC에서 작업을 이어가기 어렵습니다

→ 그래서 원격 저장소(GitHub)가 필요합니다.

## Repository & Remote

```
로컬 저장소 (내 컴퓨터 안의 Git 폴더)
     │  push →
     │  ← pull
GitHub (Remote, 클라우드에 있는 원격 저장소)
```

- **push**: 로컬의 변경사항을 GitHub로 올리기
- **pull**: GitHub의 최신 내용을 로컬로 받아오기

## PR과 Issue — 지금은 개념만

:::info Pull Request (PR)
코드 변경을 제안하고 리뷰받는 절차. 나중에 여러 명이 협업할 때 핵심적으로 사용합니다.
:::

:::info Issue
버그나 할 일을 기록하고 논의하는 게시판. 오늘은 개념만 짚고 넘어갑니다.
:::

오늘은 push / pull 중심으로 실습하고, PR·Issue는 다음 협업 과정에서 다룹니다.

## 실습 ③ GitHub에 저장소 만들기

1. GitHub 로그인 후 우측 상단 `+` 버튼 클릭
2. "New repository" 선택
3. 저장소 이름 입력 후 "Create repository" 클릭

## 실습 ④ 로컬 → GitHub로 push

```powershell
git remote add origin https://github.com/사용자명/저장소명.git
git push -u origin main
# 이후에는 git push 만으로 반영됩니다
```

:::tip
push 완료 후 GitHub 웹페이지를 새로고침하면 파일이 보입니다.
:::

---

**다음:** [Section 3. AI 도구 CLI 설치 & 실습](./ai-cli)
