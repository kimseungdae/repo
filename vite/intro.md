vite는 (프랑스어로 빠르다)라는 소리라고 한다.  
이걸 만든 에반유는 홍콩사람이다.... 근데 왜 굳이 프랑스어로 빠르다라고 했을까?  
중국어로 Kuaisude.js 뭐 이런식으로 했어야 하지 않을까?

무튼.. 네이티브 [ES Module](#es-module이란--featbard)을 넘어 더욱 다양한 기능을 제공한다고 한다.
다양한기능???
[Hot Module Replacement(HMR)](#vitejs-hot-module-replacement-hmr-이란) 같은 것들 이란다.. 이게뭔데?

벌들링 시, Rollup 기반의 다양한 빌드 커맨드를 사용할수 있데,  
[Rollup](#rollupjs란)은 또 뭔데?

어찌됬든 뭔가 빠르고 좋다니깐.. 한번 써보자고


## 1. 일단 프로젝트 만들어보자.
```
$ npm create vite@latest
```
이러면 기본적으로 가장 최신 정식버전을 땡기지롱!
근데 템플릿을 지정할수도 있네.
```
# npm 7+, '--'를 저거 꼭 붙여야됨
npm create vite@latest my-vue-app -- --template vue

# yarn
yarn create vite my-vue-app --template vue

# pnpm
pnpm create vite my-vue-app --template vue

# bun
bunx create-vite my-vue-app --template vue
```

역시나.. 에반유는 vue 만든사람이라 예제도 vue 템플릿이네..
하지만 나는 react를 사용하고, pnpm을 좋아하니깐 아래와 같은
명령어로 사용했지.

```
pnpm create vite my-project --template react
```
이것 말고도 다른 템플릿을 아래와 같은 것들도 사용할 수 있네. 
vanilla, vanilla-ts, vue, vue-ts, react, react-ts, react-swc, react-swc-ts, preact, preact-ts, lit, lit-ts, svelte, svelte-ts, solid, solid-ts, qwik, qwik-ts.

---
## 커뮤니티 템플릿
위에 템플릿 말고도 Awesome-vite templates같은 것들이 있는데,
degit를 이용해서 설치하면됨
```
npx degit user/project my-project
cd my-project

npm install
npm run dev
```
일단 지금은 관심 없으니 제외(쭉 없을것 같긴한데...)   

## 신기한 index.html의 위치..
Vite 프로젝트를 보면 index.html파일이 요상한데 있다.  
이건 의도된거라고 하네.. 번들링 없이 index.html 파일이 앱의 진입점이 되게끔 하기 위한거래..  
(어찌됬든 자동으로 변화하기 위한 방법이라는 소리자나.) 

## 커맨드 라인 인터페이스
```
{
  "scripts": {
    "dev": "vite", // 개발 서버를 실행합니다. (`vite dev` 또는 `vite serve`로도 시작이 가능합니다.)
    "build": "vite build", // 배포용 빌드 작업을 수행합니다.
    "preview": "vite preview" // 로컬에서 배포용 빌드에 대한 프리뷰 서버를 실행합니다.
  }
}
```


### 무튼 그외
릴리즈되지 않은 Vite사용하기 인데 굳이 관심없어서 제외

---
### ES Module이란 ? (feat.bard)
ECMAScript 2015(ES6)에서 도입된 모듈 시스템이다.
기존의 javascript 에서 사용되던 전역 변수나 함수를 사용하지 않고,
모듈 단위로 코드를 관리 할 수 있도록 한다.

ES Module의 특징 
=> 모듈 간의 의존성 관리
 - 모듈 간의 의존성을 명시적으로 선언할 수 있다. 이를 통해 모듈 간의 의존성을 쉽게 추적하고, 모듈의 재사용성을 높일 수 있다.
=> 모듈의 코드 분리
 - 모듈 단위로 코드를 분리할 수 있다. 이를 통해 코드의 가독성과 유지보수성을 높일 수 있다.
=> 모듈의 보안 강화
 - 모듈의 코드를 외부에서 참조하지 못하도록 하는 보안 기능을 제공한다. 이를 통해 모듈의 보안을 강화할 수 있다.

ES Module은 다음과 같은 방법으로 사용할 수 있다.

import 키워드 사용

```
// 모듈 1
export function add(a, b) {
  return a + b;
}

// 모듈 2
import { add } from "./module1";

const result = add(1, 2);
console.log(result); // 3
```

export 키워드 사용
```
// 모듈 1
export function add(a, b) {
  return a + b;
}

// 모듈 2
import { add } from "./module1";

const result = add(1, 2);
console.log(result); // 3
```

이미 알고 있는 내용이지만, 누군가에게 설명한다는 건 참 어려운 거다.
이론을 완전히 정리해서 머리속에 꼭꼭 넣어두자.

### vite.js Hot Module Replacement, HMR 이란?
웹 어플리케이션을 실행 중에도 모듈을 업데이트 할수 있단다.  
이를통해서 코드를 수정하면 즉시 업데이트 되는 화면을 볼수 있다능!?  

Hot module은 다음과 같은 특징이 있네.
ES Module을 기반으로 하지
그래서 기본적으로 ES Module을 사용하는 웹 애플리케이션에서만 사용가능해.

vite.js Hot module은 다양한 api를 제공해
이를 통해 개발자는 hmr을 보다 세밀하게 제어할 수 있지.

vite.js hot module을 사용하려면 다음과 같은 방법으로 설정하면 되지.

```
vite.config.js

export default{
  hmr: true //개쉽네?
}
```

vite.js Hot module을 사용하면 아래와 같은 뻔한 장점이 생기겠네.  
- 개발 효율성 향상. (웹서버 올려놓고도 코드 수정하고 다시 서버 재기동 안해도 화면 보니깐 개꿀)
- 사용자 경험 향상 (뭐 똑같은 소리긴 한데, 실제 서비스 올리면 사용자도 모르게 쑝하고 바뀌게 할수 있다는 소리지)

### Rollup.js란?
Javascript 모듈 번들러야...
위에 이야기 하는 모듈들 있지.. 그걸 파일 하나로 합치거나 다른 모듈로 분리할 수 있지
뭐 번들러는 이것저것 있긴 한다. 그냥 이게 쩜 있기있나보구먼
효육적이고, 유연하고, 다양한 모듈을 지원하고, 뭔가 추상적인데.. 갈길이 머니깐 나중에 정말 심심할때
찾아보자..