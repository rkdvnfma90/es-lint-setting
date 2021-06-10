# Eslint airbnb Setting

`ESlint`는 자바스크립트 표준 ECMAScript를 Lint 하여 코딩스타일을 표준화 하기 때문에 협업할 때 동일한 스타일의 코드를 유지할 수 있다.
코딩 스타일 뿐만 아니라 코드를 포맷팅 해주는 도구도 필요하다. ESlint에도 기능이 존재하지만 `Prettier`가 코드 포맷팅에 대해 더 특화되어 있으므로 이것을 사용해 보겠다. 주의할 점은 ESlint와 Prettier가 서로 겹치는 부분이 있기 때문에 이 부분을 비활성화 해야 한다.

<br/>
<br/>

## 설치

<br/>

### ESlint

- eslint : ESlint 코어
- eslint-config-airbnb : Airbnb ESlint 스타일
- eslint-plugin-import: import/export 구문을 지원
- eslint-plugin-react : 리액트 지원
- eslint-plugin-jsx-a11y : 접근성 지원
- eslint-plugin-react-hooks : 리액트 훅 지원

`만약 cra로 프로젝트를 생성하였다면 ESlint가 내장되어 있으므로 설치하지 않아도 된다. 단 airbnb 관련 eslint 라이브러리들은 설치하도록 하자`

<br/>

```javascript
npm info "eslint-config-airbnb@latest" peerDependencies
```

eslint-config-airbnb는 다른 패키지들을 의존성으로 가지고 있기 때문에 해당 명령어로 버전을 확인하여 설치 해야 한다.

<br/>

```javascript
npx install-peerdeps --dev eslint-config-airbnb
```

또는 프로젝트 경로에서 위 명령어로 한번에 설치할 수 있다.

<br/>
<br/>

### Prettier

- eslint-config-prettier: ESLint의 포맷팅 비활성화
- eslint-plugin-prettier: 포맷팅 규칙은 Prettier를 사용한다

<br/>

```javascript
npm i -D eslint-config-prettier eslint-plugin-prettier prettier
```

<br/>
<br/>

## ESlint 설정

`.eslintrc` 파일을 프로젝트 루트 경로에 만들고 하나씩 설정한다.

```javascript
{
  "extends": ["airbnb", "plugin:prettier/recommended"],
  "plugins": ["prettier"]
}
```

`extends`는 설정파일들을 확장한다는 개념으로 이해 하면 된다. 배열에 요소로 들어 있는 설정 파일들을 사용한다는 의미이다.
`plugins`는 사용자가 명시적으로 필요한 것들을 적어 준다.

<br/>

```javascript
{
  "env": {
    "browser": true,
    "jest": true
  }
}
```

`env`는 ESlint가 글로벌 객체를 인식할 수 있도록 설정하는 부분이다. `browser`를 `true`로 설정하면 `window, document`를 인식할 수 있다. 만약 jest를 사용한다면 jest에도 true 값을 설정하자.

<br/>

```javascript
{
    "ignorePatterns": ["node_modules/"]
}
```

`ignorePatterns`은 ESlint를 적용하지 않을 경로나 파일을 명시한다.

<br/>

```javascript
{
    "settings": {
    "import/resolver": {
      "node": {
        "paths": ["src"]
      }
    }
  }
}
```

이 부분은 절대경로를 사용할 때 src 폴더부터 시작하기 때문에 `import` 사용시 에러가 발생할 수 있다.
`settings`는 모든 규칙에 의해 공유되는 설정을 의미하고, `import/resolver`는 `eslint-plugin-import`의 경로설정 옵션이다.
노드에서 사용하는 `src`를 적어주면 절대 경로를 인식한다.

<br/>

```javascript
{
    "rules": {
    "react/jsx-filename-extension": ["warn", { "extensions": [".js", ".jsx"] }]
}
```

`rules`는 세부적으로 개발자가 입맛에 맞게 설정할 수 있다.

- off (0) : 규칙을 끈다.
- warn (1) : 경고를 띄운다.
- error (2) : 에러를 띄운다.

<br/>
<br/>

## Prettier 설정

`.prettierrc` 파일을 프로젝트 루트 경로에 만든다.

```javascript
{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80
}

```
