## Next js, typescript, redux-toolkit, styled components with tailwind 보일러플레이트



### next js 설치

```
npx create-next-app@latest --ts
```

### ES Lint 설정

- ES : ES는 ECMA Script 와 동일하며, ECMA Script란 ECMA-262 기술 규격에 정의된 표준화된 스크립트 프로그래밍 언어. 자바스크립트를 표준화하기 위해 만들어진 규격
- 린트(lint) 또는 린터(linter)는 소스 코드를 분석하여 프로그램 오류, 버그, 스타일 오류, 의심스러운 구조체에 표시(flag)를 달아놓기 위한 도구

1. **typesciprt ESlint 설치**

```
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-import-resolver-typescript
```

- parser:
- resolver:
- plugin :

1. **airbnb ESLint 설치**

```
npx install-peerdeps --dev eslint-config-airbnb
npm install eslint-config-airbnb-typescript
//.eslintrc.js

module.exports = {
  root: true,
  parser: "@typescript-eslint/parser",
  plugins: ["@typescript-eslint", "prettier"],
  parserOptions: {
    project: "./tsconfig.json",
  },
  env: {
    node: true,
  },
  extends: [
    "plugin:@typescript-eslint/recommended",
    "airbnb",
    "airbnb-typescript",
    "plugin:prettier/recommended",
  ],
  rules: {
    // 'React' must be in scope when using JSX 에러 지우기(Next.js)
    "react/react-in-jsx-scope": "off",
    // ts파일에서 tsx구문 허용(Next.js)
    "react/jsx-filename-extension": [1, { extensions: [".ts", ".tsx"] }], //should add ".ts" if typescript project
  },
};
```

2. **prettier 설치**

```
npm install --save-dev eslint-config-prettier
```

- 설정

```
//ESLint config
{
  "extends": ["next", "prettier"]
}
// airbnb 스타일 가이드, .prettier
module.exports = {
  printWidth: 80, //코드 한줄 최대치
  semi: true, //코드 마지막에 세미콜론
  singleQuote: false, //문자열을 작은따옴표로 작성할것인지(false = 큰 따옴표)
  trailingComma: 'all', //객체나 배열 등에 맨 마지막에도 콤마
  tabWidth: 2, //들여쓰기 2칸(스페이스 2칸)
  bracketSpacing: true, //객체 리터럴에서 괄호에 공백 삽입 여부
  endOfLine: 'auto',
  useTabs: false, //탭 대신 스페이스
  arrowParens: 'avoid', // 화살표 함수에서 매개변수를 하나만 받을때 괄호 생략
};
```

3. **styled components 설치**

```
npm install --save styled-components
npm i --save-dev @types/styled-components
npm install --save-dev babel-plugin-styled-components
```

- Next.js 12이상 설정

```json
// 바벨에 설정 추가
{
  "presets": ["next/babel"],
  "plugins": [["styled-components", { "ssr": true }]]
}
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: false,
  compiler: {
    styledComponents: true,
  },
};

module.exports = nextConfig;
```

⇒ styled components는 javascript 로딩 이후 css 작동됨. SSR에서 추가 설정 필요

4. **tailwind css 설치**

```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

- 설정

```jsx
// tailwind.config.js

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
// global.css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

5. **axios 설치**

```
npm install axios
```

6. **redux toolkit 설치**

```
npm install react-redux
npm install @reduxjs/toolkit
npm i @types/react-redux
```

- ssr을 위한 redux-wrapper 설치

```
npm install next-redux-wrapper --save
```

`* 상세 코드는 store > index.ts 참고`
