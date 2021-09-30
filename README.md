# 목표
- eslint와 prettier의 설정을 적용한다.
- eslint와 prettier 동시 설정시 발생하는 충동을 테스트 한다.
- 코드 검출은 ESLint가 하고, 포매팅은 Prettier가 담당하도록 설정한다.
    - 단 ESLint의 포매팅 기능은 충돌되지 않아야 한다.

## 설명

### `ESLint`
- ES(EcmaScript) + Lint의 합성어
- ESLint는 JavaScript의 스타일 가이드를 따르지 않거나 문제가 있는 안티 패턴들을 찾아주고 일관된 코드 스타일로 작성하도록 도와준다.

### `Prettier`
- 기존의 코드에 적용되어있던 스타일들을 전부 무시하고, 정해진 규칙에 따라 자동으로 코드 스타일을 정리해 주는 Code Formatter 이다.

### 차이점
| ESLint | Pretter |
| --- | --- |
| 문법 에러 검출 | 코딩 스타일 일관성 |

### 함께 설정할 경우 문제점
- ESLint는 코드 분석기 이지만 formatting 관련 규칙들이 있다.
- 만약 ESLint와 Prettier를 같이 사용한다면 **포매팅 충돌 문제**가 발생할 수 있다.
- 이를 위해서 추가 설정이 필요하다.


## eslint + prettier 설정 비교

### pritter 설정 끄고 테스트
```javascript
// .eslintrc.js

extends: [
    '@nuxtjs',
    'plugin:nuxt/recommended'
    // 'prettier'
],
```
- vue 파일에서 규칙 오류를 잡아내고 저장시 자동 보정 됨
- `.eslintrc.js`의 `rules` 설정여부와 상관 없음
- 만약 `extends`의 `'prettier'`를 활성화 하면 `linter` 동작 안 함

## 최종 설정 방법
> (nuxt-app CLI를 통한 프로젝트 생성시)

### 프로젝트 생성
```bash
$ npm init nuxt-app {프로젝트명}
```
- 옵션에서 `eslint`, `prettier` 기본 선택

### 프로젝트 생성 후 기본값
```javascript
// .eslintrc.js

extends: [
    '@nuxtjs',
    'plugin:nuxt/recommended',
    'prettier'
],
```

```json
// package.json

  "devDependencies": {
    "@babel/eslint-parser": "^7.14.7",
    "@nuxtjs/eslint-config": "^6.0.1",
    "@nuxtjs/eslint-module": "^3.0.2",
    "eslint": "^7.29.0",
    "eslint-config-prettier": "^8.3.0",
    "eslint-plugin-nuxt": "^2.0.0",
    "eslint-plugin-vue": "^7.12.1",
    "prettier": "^2.3.2"
  }
```

### dev dependency 추가
> https://github.com/prettier/eslint-plugin-prettier#recommended-configuration
```bash
$ npm install --save-dev eslint-plugin-prettier
```

```json
// package.json

  "devDependencies": {
    "@babel/eslint-parser": "^7.14.7",
    "@nuxtjs/eslint-config": "^6.0.1",
    "@nuxtjs/eslint-module": "^3.0.2",
    "eslint": "^7.29.0",
    "eslint-config-prettier": "^8.3.0",
    "eslint-plugin-prettier": "^4.0.0", // 추가됨
    "eslint-plugin-nuxt": "^2.0.0",
    "eslint-plugin-vue": "^7.12.1",
    "prettier": "^2.4.1"
  }
```

### .eslintrc.js 설정 변경
#### extends 추가
```javascript
extends: [
    '@nuxtjs',
    'plugin:nuxt/recommended',
    'plugin:prettier/recommended', // 추가
],
```

#### Prettier 룰을 eslint에 적용
```javascript
rules: {
    'no-console': 'off',
    'prettier/prettier': [
        'error',
        {
            // 추가되는 룰은 이곳에 작성한다.
            singleQuote: true,
            semi: true,
            useTabs: false,
            tabWidth: 2,
            trailingComma: 'all',
            printWidth: 80,
            bracketSpacing: true,
            arrowParens: 'avoid',
        },
    ],
},
```

> `.prettierrc` 파일은 삭제한다.

