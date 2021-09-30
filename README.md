# 목표
- eslint와 prettier의 설정을 적용한다.
- eslint와 prettier 동시 설정시 발생하는 충동을 테스트 한다.
- 파일 저장시 자동 포매팅, 문법 교정이 이루어져야 한다.

## 설명

### `ESLint`
- ES(EcmaScript) + Lint의 합성어
- ESLint는 JavaScript의 스타일 가이드를 따르지 않거나 문제가 있는 안티 패턴들을 찾아주고 일관된 코드 스타일로 작성하도록 도와준다.

### `Prettier`
- 기존의 코드에 적용되어있던 스타일들을 전부 무시하고, 정해진 규칙에 따라 자동으로 코드 스타일을 정리해 주는 Code Formatter 이다.

### 차이점
| ESLint | Pretter |
| --- | --- |
| 문접 에러 잡기 | 코딩 스타일 일관성 |

### 같이 설정할 경우 문제점
- ESLint는 코드 분석기 이지만 formatting 관련 규칙들이 있다.
- 만약 ESLint와 Prettier를 같이 사용한다면 포매팅 충돌 문제가 발생할 수 있다.
- 이를 위해서 추가 설정이 필요하다.


## eslint + prettier 설정 비교

### pritter 설정 끔
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