정리된 노션 링크입니다: https://boom-passbook-4e2.notion.site/Scope-dedbab839b3e46dcbb4206205da40ef5

# Scope

<aside>
1️⃣ **Scope란 무엇인가요?**

---

규칙에 따라 식별자(변수, 함수, 클래스)에 접근할 수 있는 범위가 존재하는데, 이 식별자 접근 규칙에 따른 유효 범위를 스코프라고 합니다. 스코프에는 Block Scope와 Function Scope가 있습니다.

</aside>

<aside>
2️⃣ **다음 코드의 결과를 예측하고 이유를 설명해주세요.**

```jsx
var name = 'zero';
function log() {
  console.log(name);
}

function wrapper() {
  var name = 'nero';
  log();
}
wrapper();
```

---

출력되는 결과는 zero입니다.

`log()`가 `wrapper()`안에서 호출되었더라도, `log()` 내부 변수는 `log()`를 처음 선언 했을 때를 기준으로 가장 가까운 스코프에 있는 전역 변수 `name`을 참고하기 때문입니다.

</aside>

## 학습 내용

; 변수에 접근할 수 있는 범위

; 식별자 접근 규칙에 따른 유효 범위

Javascript에서는 식별자(변수, 함수, 클래스)에 접근할 수 있는 범위가 존재하는데, 이 식별자 접근 규칙에 따른 유효 범위를 스코프라고 한다.

<aside>
🔦 **Scope의 주요 규칙**

---

1. 안쪽 스코프 → 바깥쪽 스코프 🆗 but 반대는 불가능하다.
    
    바깥쪽 스코프에서 선언한 식별자는 안쪽 스코프에서 사용 가능하다.
    
    #Scope Chain
    
2. 중첩 가능
3. 전역Global 스코프 & 지역Local 스코프
    
    `Global Scope`: 가장 바깥쪽의 스코프
    
    `Local Scope`: 그 외 스코프
    
4. 우선 순위: 지역 변수 > 전역 변수
</aside>

## Block Scope

; `{ }` 단위 Scope

- 화살표 함수는 블록 스코프로 취급된다.

```jsx
function print() { // 함수 블록
 console.log(a);
}
{ // 블록
 const a = '1';
}
```

## Function Scope

; 함수 단위 Scope

- JavaScript는 function scope가 default이다.

```jsx
function scopeTest(){
	var a =0;
	if(true){
		var b =0;
		for(varc =0;c<3;c++){
			console.log("c="+c);
		}
		console.log("c="+c);
	}
	console.log("b="+b);
}
// c = 0
// c = 1
// c = 2
// c = 3
// b = 0
```

## 변수명 중복 허용: Scope Chain

현재 자신의 scope에서 사용하고자 하는 변수가 없다면 Scope Chain을 통해 더 바깥쪽의 스코프에서 해당 변수를 찾는다.

아래 두 코드의 결과를 예측해보자.

코드 출처: [https://www.zerocho.com/category/JavaScript/post/5740531574288ebc5f2ba97e](https://www.zerocho.com/category/JavaScript/post/5740531574288ebc5f2ba97e)

```jsx
var x = 'global';
function ex() {
  var x = 'local';
  x = 'change';
}
ex(); // x를 바꿔본다.
alert(x); // 여전히 'global'
```

```jsx
var x = 'global';
function ex() {
  x = 'change';
}
ex();
alert(x); // 'change'
```

1번 코드의 경우 x는 여전히 global 이지만 2번 코드는 change로 바뀐다.

함수 스코프로 인해 1번 코드의 x는 전역 변수를 바꿀 수 없지만, 2번 코드에서는 함수 안에서 x를 선언하지 않았기 때문에 스코프 체인을 통해 찾은 전역 변수 x의 값을 변경할 수 있게 된 것이다.

## Lexical Scoping 정적 스코프

스코프는 함수를 호출할 때가 아닌 선언할 때 생기는 것이다.

아래 코드의 결과를 예상해보자

코드 출처: [https://www.zerocho.com/category/JavaScript/post/5740531574288ebc5f2ba97e](https://www.zerocho.com/category/JavaScript/post/5740531574288ebc5f2ba97e)

```jsx
var name = 'zero';
function log() {
  console.log(name);
}

function wrapper() {
  name = 'nero';
  log();
}
wrapper();
```

```jsx
var name = 'zero';
function log() {
  console.log(name);
}

function wrapper() {
  var name = 'nero';
  log();
}
wrapper();
```

`log()` 안의 `name`은 전역변수 `name`을 가리키고 있으므로 첫번째 코드는 nero, 2번째 코드는 zero가 출력된다. 즉, 함수를 처음 선언하는 순간, 함수 내부의 변수는 자기 스코프로부터 가장 가까운 곳(상위 범위에서)에 있는 변수를 계속해서 참조하게 되기 때문이다. 그래서 2번 코드에서 `wrapper()` 안에서 `log()`를 호출해도 지역변수 `name`이 아닌 전역변수 `name`을 참조한다.

# var, let, const

<aside>
1️⃣ **var, let, const의 차이점을 설명해주세요.**

---

var과 let은 둘 다 재할당이 가능하다는 공통점이 있지만 var은 재선언이 가능하고, let은 재선언을 할 수 없습니다. 그와 달리 const는 재선언과 재할당이 모두 불가능합니다.

또한, var은 함수 스코프를 따르지만 let과 const는 블록 스코프를 따른다는 점에서 차이가 있습니다.

</aside>

<aside>
2️⃣ **var과 let 중 무엇을 더 선호하는지, 그 이유는 무엇인지 설명해보세요.**

---

저는 let 사용을 더 선호합니다.

var은 재선언과 재할당이 모두 가능합니다. 또한 함수 스코프 만을 따르는 var로 변수를 선언할 경우, 지역 스코프로 선언한 변수가 전역 스코프에서도 접근, 참조가 가능해지므로 예측하지 못한 오류가 발생할 가능성이 큽니다. 그래서 더 예측 가능한 코드를 작성하기 위해 블록 단위로 스코프가 구분되는 let 사용을 더 선호하게 되었습니다.

</aside>

<aside>
3️⃣ **전역 변수를 지양해야 하는 이유는 무엇인가요? 어떻게 하면 전역 변수 사용을 줄일 수 있나요?**

---

전역 변수는 어디서든 접근이 가능해서 의도치 않은 로직으로 인한 문제가 발생하기 쉽기 때문에 자제 해야합니다. 특히 전역 변수를, 블록 스코프를 무시하고 재선언과 재할당이 가능한 var로 선언하는 경우 문제가 더욱 심화될 수 있습니다.

이를 해결하기 위해서는 변수를 함수 안에 넣어 지역 변수로 만들거나 네임스페이스(객체 안에 속성)로 만들면 됩니다. 하지만 네임스페이스 내의 변수도 외부에서 접근하여 쉽게 바꿀 수 있기 때문에 함수로 감싼 후 공개할 변수만 return하는 방법도 사용할 수 있습니다.

[https://www.zerocho.com/category/JavaScript/post/5740531574288ebc5f2ba97e](https://www.zerocho.com/category/JavaScript/post/5740531574288ebc5f2ba97e)

</aside>

<aside>
4️⃣ **다음 코드의 결과를 예측해보세요. 그리고 그 이유가 무엇인지 설명해보세요.**

```jsx
console.log (greeter);
var greeter = "say hello"
```

```jsx
console.log (greeter);
let greeter = "say hello"
```

---

첫 번째 코드에서는 undefined가 출력되고 두 번째 코드에서는 greeter가 정의되지 않았다는 Reference 에러가 발생합니다.

두 코드의 차이는 변수가 var로 선언된 것과 let으로 선언된 것입니다.

둘 다 scope의 최상단으로 호이스팅 되지만,  var은 변수 선언부가 옮겨지고 값이 undefined로 초기화되고 let은 그렇지 않기 때문에 이와 같은 차이가 발생합니다.

</aside>

## 학습 내용

## 스코프와 var, let, const 키워드

|  | var | let | const |
| --- | --- | --- | --- |
| Global Scope | ⭕️ | ❌ | ❌ |
| Local Scope | ⭕️ |  |  |
| Block Scope | ❌ | ⭕️ | ⭕️ |
| Function Scope | ⭕️ | ⭕️ | ⭕️ |
| 값 재할당 | 가능 | 가능 | 불가능 |
| 재선언 | 가능 | 불가능 | 불가능 |
- `재선언` 이란?
    
    이미 선언한 변수명을 다시 선언하는 것
    
    ```jsx
    // var로 선언한 변수 name의 재선언 
    var name = 'yoojin' ; // 변수 선언 및 초기화
    var name = 'lizzie' // 변수 재선언 가능
    
    //const 변수 재선언 
    const occupation = 'developer'; // 변수 선언 
    const occupation = 'backend developer'; // 재선언 -> 에러 :
    ```
    
    [https://stay-present.tistory.com/23](https://stay-present.tistory.com/23)
    
    대신 변수의 스코프가 다른 경우, 이런 형태가 가능해진다.
    
    ```jsx
    let feedback = "good job";
        if (true) {
            let feedback = "keep up the good work";
            console.log(feedback); // "keep up the good work"
        }
        console.log(feedback); // "good job"
    ```
    
- `재할당` 이란?
    
    ; 이미 값이 할당된 변수에 새로운 값을 할당하는 것
    
    ‼️ const로 객체 생성 시 속성 자체 변경은 불가능 but 배열 내 값이나 객체 속성 값은 업데이트 가능
    
    ```jsx
    const employees = {
            name: 'yoojin',
            age: 24
        }; // const로 employees 객체 생성 
        
    employees = {
            occupation: 'developer'
        }  // error: TypeError: Assignment to constant variable.
        
    employees.age = 28; // 객체 properties 값 업데이트는 가능
    ```
    
    [https://stay-present.tistory.com/23](https://stay-present.tistory.com/23)
    

```jsx
for(let i=0; i<3; i++){
	console.log(i);
}
console.log('final: ', i);    
// ReferenceError
```

```jsx
for(var i=0; i<3; i++){
	console.log(i);
}
console.log('final: ', i);    
// 'final: 3'
```

## var

- 기존 var: 함수 스코프 → 함수 내에서만 지역 변수가 유지되는 Issue
    
    ⇒ ES2015(ES6)에서 let, const 키워드가 추가되면서 함수가 아닌 일반 블록에서도 지역 변수 선언 가능해짐
    

<aside>
🔖 **여러가지 Cases**

---

**[ Window 객체 ]** : 브라우저에만 존재하는 객체 & 전역 영역을 담고 있다.

- 함수 선언식 / var 키워드로 변수를 선언하면 window 객체에 속해진다.

**[ 전역 변수 var ]** 

- 전역 변수를 var로 선언해서 브라우저의 내장 기능을 못하게 만들 수도 있다.
- var로 선언한 전역 변수명과 지역변수 명이 같아 충돌하는 경우, 지역 변수가 사용된다.
</aside>

## 선언 없는 변수 할당: var 키워드 생략

다른 프로그래밍 언어의 경우 변수 선언 시 변수형을 쓰지 않을 경우 에러가 나지만 JavaScript에서는 var 키워드를 생략할 수 있다.

```jsx
function scopeExam(){
	scope = 20;
	console.log("scope = "+ scope);
}

function scopeExam2(){
	console.log("scope = "+ scope);
}
scopeExam(); // 20
scopeExam2(); // 20
```

- var 키워드가 생략된 변수는 전역 변수로 선언된다.
- Strict Mode를 사용하면 “선언 없는 변수 할당”을 에러로 판단해준다.
    
    ; `use strict`
    

## 호이스팅과 var, let, const

`호이스팅`: 코드 실행 전에 변수의 선언과 함수의 선언이 각 스코프의 맨 위로 옮겨지는 자바스크립트 매커니즘

|  | var | let | const |
| --- | --- | --- | --- |
| 호이스팅 위치 | scope 최상단 | scope 최상단 | scope 최상단 |
| 값 초기화 | undefined | ❌
→ TDZ 발생 | ❌
→ TDZ 발생 |

### TDZ란?

![출처: [https://noogoonaa.tistory.com/78](https://noogoonaa.tistory.com/78)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ea23013e-104d-4da7-a234-9dc1432639fc/Untitled.png)

출처: [https://noogoonaa.tistory.com/78](https://noogoonaa.tistory.com/78)

; Temporal Dead Zone ; 일시적인 사각지대

; 스코프의 시작 지점 ~ 초기화 시작 지점의 구간

```jsx
console.log (greeter);
var greeter = "say hello"

=========================
var greeter;
console.log(greeter); //  undefined
greeter = "say hello"
```

var로 선언한 변수는 변수 선언 전에 사용하려고 할 때 에러를 받지 않고 undefined를 받는다.

```jsx
console.log (greeter); // ReferenceError: greeter is not defined
const greeter = "say hello"
    
console.log (greeter); // ReferenceError: greeter is not defined
let greeter = "say hello"
```

반면에 const와 let을 사용하는 경우 값이 초기화 되지 않아 변수 선언 전에 사용하려고 하면 참조 에러를 받는다. ⇒ 이 기간을 `TDZ`라고 한다.

# 참고 자료

[[JavaScript] 스코프(Scope)와 변수 선언 (var, let, const 키워드 차이점) - 하나몬](https://hanamon.kr/javascript-스코프와-변수선언키워드-차이점/)

[Scope, let/const/var의 차이점](https://joooing.tistory.com/entry/Scope)

[(JavaScript) 스코프(Scope)란?](https://medium.com/@su_bak/javascript-스코프-scope-란-bc761cba1023)

[javascript - const/ let / var 차이점 (재선언, 재할당, 유효범위, 호이스팅의 관점에서)](https://stay-present.tistory.com/23)

[(JavaScript) 함수의 범위(scope) - lexical scoping](https://www.zerocho.com/category/JavaScript/post/5740531574288ebc5f2ba97e)

[JavaScript : Scope 이해](https://www.nextree.co.kr/p7363/)
