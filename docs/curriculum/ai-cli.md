---
id: ai-cli
title: "Section 3. AI 도구 CLI 설치 & 실습"
sidebar_position: 4
description: 터미널에서 바로 AI에게 코드를 시키다 · 1시간
---

# Section 3. AI 도구 CLI 설치 & 실습

> 터미널에서 바로 AI에게 코드를 시키다 · 1시간

## 터미널에서 바로 AI에게 코드를 시키다

웹 채팅창이 아니라, 터미널에서 AI가 직접 내 폴더의 파일을 읽고 수정합니다.

```powershell
ai "예산 합계 계산 함수에 천단위 콤마를 추가해줘"

# > budget.gs 파일을 확인하는 중...
# > formatNumber() 함수를 수정했습니다.
# > 변경사항을 확인하시겠습니까? (git diff)
```

## 실습 ⑤ 설치 & 인증

1. 설치 명령어 실행
2. 브라우저에서 계정 로그인 / 인증
3. 터미널에서 인증 완료 메시지 확인

## 실습 ⑥ AI에게 작업 시켜보기

```powershell
ai "이 폴더의 test.gs 파일에 콘솔 로그를 추가해줘"

# > test.gs 를 수정했습니다.

git diff        # 무엇이 바뀌었는지 확인
git add . && git commit -m "로그 추가"
```

## AI가 고쳤다고 바로 믿지 마세요

```
git diff 로 변경사항 확인  →  의미 단위로 나눠서 커밋
```

:::tip
한 번에 여러 가지를 고쳤어도, 검토 후 나눠서 커밋하면 나중에 되돌리기 쉬워집니다.
:::

---

**다음:** [Section 4. Google AppScript 프로젝트 관리](./clasp-appscript)
