# angular-studypie-study

studypie에서 8주동안 진행되었던 angular study 내용을 정리한 곳입니다.

## 타입스크립트 오버뷰

https://slides.com/woongjae/deck-8#/1/2

타입스크립트 : Compiled Language (Transpile)

## 개발 환경 구축 및 컴파일러 사용

- node(https://nodejs.org/ko), 브라우저

###### IDE

- Visual Studio Code
- IntelliJ IDEA / WebStorm

tsc --init 명령어 - tsconfig.json 생성

tsc -w 명령어 - watch 모드 -> 코드 변경시 컴파일

## IDE 활용

- VSCode는 타입스크립트 내장됨.
- 내장된 컴파일러를 선택할수 있고, 직접 설치한 컴파일러를 선택할 수 있음

npm i typescript tslint

VSC tslint 확장프로그램 있음.

Your JavaScript is TypeScript (https://basarat.gitbooks.io/typescript/content/docs/javascript/recap.html)

## Compiler Options

http://json.schemastore.org/tsconfig

**최상위 프로퍼티**

- compileOnSave
- extends
- compileOptions
- files
- include
- exclude

**compileOnSave**

- 저장하면 자동으로 컴파일
- true / false (default false)
- 최상단에 설정해야 한다 ?

**extends**

- 공통적인 면들이 많은 ts파일에 사용?
- 파일 (상대) 경로명 : string

**files, include, exclude**

- 셋다 설정이 없으면, 전부다 컴파일
- files
  - 상대 혹은 절대 경로의 리스트 배열임
  - exclude 보다 쎔
- include, exclude
  - glob 패턴 (마치 .gitnore)
  - include
    - exclude 보다 약함
    - - 같은걸 사용하면, .ts/.tsx/.d.ts 만 include (allowJS)
  - exclude
    - 설정 안하면 4가지 (node_modules, bower_components, jspm_pakages, <outDir>)를 default로 제외함
    - <outDir>은 항상 제외함 (include에 있어도)

**CompilerOptions**

_@types_

- TypeScript 2.0 부터 사용 가능해진 내장 type definition 시스템
- 아무 설정을 안하면?
  - node_modules/@types 라는 모든 경로를 찾아서 사용
- typeRoots를 사용하면?
  - 배열 안에 들어있는 경로들 아래서만 가져옴.
- types를 사용하면?
  - 배열 안의 모듈 혹은 ./node_modules/@types/ 안의 모듈 이름에서 찾아옴.
  - [] 빈 배열을 넣는다는건 이 시스템을 이용하지 않겠다는 것임.
- typeRoots 와 types 를 같이 사용하지 않음.

_target 과 lib_

- target
  - 빌드의 결과물을 어떤 버전으로 할 것이냐
  - 지정을 안하면 es5임.
- lib
  - 기본 type definition 라이브러리를 어떤 것을 사용할 것이냐
  - lib 를 지정하지 않을 때,
    - target 이 'es5'이고, 디폴트로 dom, es5, scripthost 를 사용함
    - target 이 'es6'이면, 디폴트로 dom, es6, dom.iterable, scripthost 를 사용함
  - lib 를 지정하면 그 lib 배열로만 라이브러리를 사용함
    - 빈 [] => 'no definition found 어쩌구'

_outDir, outFile_

_module_

- module
  - 컴파일 된 모듈의 결과물을 어떤 모듈 시스템으로 할지 결정
  - target 이 'es6' 이면 es6가 디폴트이고,
  - target 이 'es6' 가 아니면 commonjs 가 디폴트임.
  - AMD 나 System 와 사용하려면, outFile 이 지정되어야 함
  - ES6 나 ES2015 를 사용하려면, target 이 es5 이하여야 함
- moduleResolution
  - ts 소스에서 모듈을 사용하는 방식을 지정해야 함.
  - Classic 아니면 Node 라고 생각하시면 됨
  - CommonJS 일때만 Node 라고 생각하시면 됨
- paths 와 baseUrl
  - 상대경로 방식이 아닌 baseUrl로 꼭지점과 paths 안의 키/밸류로 모듈을 가져가는 방식임
- rootDirs: 배열 안에서 상대 경로를 찾는 방식임.
