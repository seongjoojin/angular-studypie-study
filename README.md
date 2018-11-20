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

## TypeScript Basic Types

- Typescript 에서 프로그램 작성을 위해 기본 제공하는 데이터 타입
- **사용자가 만든 타입은 결국은 이 기본 자료형들로 쪼개짐.**
- Javascript 기본 자료형을 포함 (superset)
    - ECMAScript 표준에 따른 기본 자료형은 6가지
        - Boolean
        - Number
        - String
        - Null
        - Undefined
        - Symbol (ES6에 추가)
        - Array :  object 형
    - 프로그래밍을 도울 몇가지 타입이 더 제공됨
        - Any
        - Void
        - Never
        - Enum
        - Tuple : object 형

#### Primitive Type

- 오브젝트와 레퍼런스 형태가 아닌 실제 값을 저장하는 자료형임
- 프리미티브 형의 내장 함수가 사용 가능한것은 자바스크립트 처리 방식 덕분

```typescript
let name = 'mark';

name.toString();
```

#### literal ?

- 값 자체가 변하지 않는 값을 의미함.
- 상수와 다른 것은 상수는 가리키는 포인터가 고정이라는 것이고, 리터럴은 그 자체가 값이자 그릇임.

```
35; // number 리터럴
'mark'  // string 리터럴
true    // boolean 리터럴

// object 리터럴
{
    name: 'mark',
    age: 35
}
```
#### Boolean / boolean

- 가장 기본적인 데이터 타입
- 단순한 true 혹은 false 값 임
- javascript / TypeScript 에서 'boolean'이라고 부른다

#### Number / number

- Javascript 와 같이, TypeScript 의 모든 숫자는 부동 소수점 값임
- TypeScript 는 16진수 및 10진수 리터럴 외에도, 2진수 및 8진수를 지원함

#### String / string

- 다른 언어에서와 마찬가지로 텍스트 형식을 참조하기 위해 'string'형식을 사용함
- 문자열 데이터를 둘러싸기 위해 큰 따옴표(")나, 작은 따옴표(')를 사용함

#### Template String

- 행에 걸쳐 있거나, 표현식을 넣을 수 있는 문자열
- 이 문자열은 backtick(=backquote) 기호에 둘러쌓여 있음
- 포함된 표현식은 '${expr}'와 같은 형태로 사용함

#### undefined & null

- TypeScript 에서 'undefined'와 'null'은 실제로 각각 'undefined'와 'null'이라는 고유한 타입을 가짐
- 'void'와 마찬가지로, undefined 와 null 은 그 자체로는 쓸모가 없음
- 둘다 소문자만 존재함.

#### undefined & null are subtypes of all other types.

- 기본 설정이 그렇다
- number 에 null 또는 undefined 를 할당할 수 있다는 의미임
- 하지만, 컴파일 옵션에서 '--strictNullChecks' 사용하면, null 과 undefined 는 void 나 자기 자신들에게만 할당할 수 있음.
    - 이 경우, null 과 undefined 를 할당할 수 있게 하려면, union type 을 이용해야 함.
    
#### null in JavaScript

- null 이라는 값으로 할당된 것을 null 이라고 함.
- 무언가가 있는데, 사용할 준비가 덜 된 상태.
- null 이라는 타입은 null 이라는 값만 가질 수 있음.
- 런타임에서 typeof 연산자를 이용해서 알아내면, object 임.

#### undefined in JavaScript

- 값을 할당하지 않은 변수는 undefined 라는 값을 가짐.
- 무언가가 아예 준비가 안된 상태
- object 의 property 가 없을 때도 undefined 임.
- 런타임에서 typeof 연산자를 이용해서 알아내면, undefined 임.

#### Void

- 타입이 없는 상태임
- 'any'와 반대의 의미를 가짐
- Void 는 없음. 소문자임.
- 주로 함수의 리턴이 없을 때 사용함. 그 외에는 사용할 일이 거의 없음.

#### Any

- 어떤 타입이어도 상관없는 타입임.
- 이걸 최대한 쓰지 않는게 핵심임
- 왜냐하면 컴파일 타임에 타입 체크가 정상적으로 이뤄지지 않기 때문임
- 그래서 컴파일 옵션 중에는 any 를 쓰면 오류를 뱉도록 하는 옵션도 있음
    - nolmplicitAny
    
#### Never

- 리턴에 주로 사용됨


#### Array

- 원래 자바스크립트에서 array 는 객체임
- 사용방법
    - Array<타입>
    - 타입[]
    
#### Tuple

- 배열인데 타입이 한가지가 아닌 경우
- 마찬가지로 객체임
- 꺼내 사용할때 주의가 필요함

#### Enum

- C 에서 보던것과 같음

#### Symbol

- ECMAScript 2015의 Symbol 임.
- 프리미티브 타입의 값을 담아서 사용함.
- 고유하고 수정불가능한 값으로 만들어줌
- 그래서 주로 접근을 제어하는데 쓰는 경우가 많음.