# HYU Vibe Coding

한양대학교 바이브 코딩(Vibe Coding) 방법론 교육 자료입니다. [Docusaurus](https://docusaurus.io/)로 제작되었으며, `main` 브랜치에 push 하면 GitHub Actions를 통해 자동으로 GitHub Pages에 배포됩니다.

배포 사이트: https://HYU-staff.github.io/hyu-vibe-coding-management/

## 로컬 개발

```bash
npm install
npm start
```

로컬 개발 서버가 실행되며 대부분의 변경 사항은 저장 즉시 브라우저에 반영됩니다.

## 빌드

```bash
npm run build
```

`build` 디렉토리에 정적 파일이 생성됩니다.

## 자료 추가하기

`docs/` 폴더 아래에 마크다운(`.md`/`.mdx`) 파일을 추가하면 사이드바에 자동으로 반영됩니다. 자세한 구조는 [Docusaurus 문서](https://docusaurus.io/docs/docs-introduction)를 참고하세요.

## 배포

배포는 `.github/workflows/deploy.yml`에 정의된 GitHub Actions에 의해 자동으로 처리됩니다. `main` 브랜치에 push하면 빌드 후 GitHub Pages로 배포됩니다.
