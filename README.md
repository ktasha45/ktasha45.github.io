[ktasha45.github.io](https://ktasha45.github.io/)

## 로컬 실행

Ruby 3.3과 Devkit을 설치한 환경에서 실행합니다. 설치 직후에는 터미널을 새로 열어 주세요.

```powershell
bundle install
bundle exec jekyll serve
```

브라우저에서 http://localhost:4000/ 에 접속합니다. CV 페이지는 http://localhost:4000/cv/ 에서 확인할 수 있습니다.

정적 파일만 생성하려면 `bundle exec jekyll build`를 실행합니다.

## CV 편집

`cv.html`의 맨 위 `---` 사이 설정은 유지하고, 그 아래에 HTML로 CV 내용을 작성합니다.
