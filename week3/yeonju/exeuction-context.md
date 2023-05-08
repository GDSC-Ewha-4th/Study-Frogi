정리된 노션 링크입니다: https://boom-passbook-4e2.notion.site/33f2ccdc90bf4cf8ab72fef5fa0b712b

# 실행 컨텍스트

<aside>
1️⃣ **실행 컨텍스트(Execution Context)에 대해서 설명해주세요.**

---

- 답안
    
    실행 컨텍스트는 실행 가능한 코드에 제공할 환경 정보를 모아놓은 객체입니다.
    
    해당 객체에는 변수 객체, 스코프 체인, this 정보가 담겨있습니다.
    
    자동으로 전역 컨텍스트가 생성된 후 함수 호출시마다 함수 컨텍스트가 생성되고, 컨텍스트 생성이 완료된 후에 함수가 실행됩니다. 함수 실행 중에 사용 되는 변수들을 변수 객체 안에서 값을 찾고 값이 존재하지 않는다면 Lexical 환경의 outerEnvironmentReference를 통해 Scope 체인을 따라 올라가면서 탐색합니다. 함수 실행이 마무리가 되면 해당 컨텍스트는 사라지고, 페이지가 종료되면 전역 컨텍스트도 사라집니다. 
    
</aside>

<aside>
2️⃣ **렉시컬 환경이란 무엇인가요?**

---

- 답안
    
    렉시컬 환경은 특정 코드가 선언/정의/작성된 **환경**을 의미하는 객체입니다. 
    
    환경 레코드와 외부환경레퍼런스로 나뉘는데, 
    
    환경레코드에는 현재 컨텍스트와 관련된 코드의 식별자 정보가 저장됩니다. 즉, JS 엔진은 코드가 실행되기 전에 실행 컨텍스트에 속한 변수명을 모두 알고 있는 것인데요, 이를 위해 호이스팅이 발생한다고 볼 수 있습니다. 
    
    외부환경레퍼런스는 현재 호출된 함수가 선언될 당시의 렉시컬 환경을 참조하는데, 이를 이용해서 스코프 체이닝이 가능해집니다.
    
</aside>

<aside>
3️⃣ **실행 컨텍스트의 객체에 담긴 정보는 무엇이 있나요?**

---

- 답안
    
    변수 객체, Scope 체인, this 값이 있습니다.
    
    변수 객체에는 변수, 매개변수parameter, 인수argument 정보와 함수 정보가 담겨있고, 이때 변수와 함수 표현식으로 생성된 함수는 생성은 되지만 초기화는 되지 않아 undefined 상태입니다.
    
    스코프 체인은 연결리스트 형태로 스코프 정보가 저장된 것이고,
    
    this 값에는 이 변수 객체의 this에 바인딩 할 객체를 저장합니다.
    
</aside>

<aside>
4️⃣ **자바스크립트는 어떤 언어인가요?**

---

- 답안
    
    자바스크립트는 하나의 콜스택을 갖는 단일 스레드 기반 언어이자 동적 언어입니다.
    
</aside>

## 학습 내용

## 실행 컨텍스트*Execution Context*

*실행 컨텍스트Execution Context는 scope, hoisting, this, function, closure 등과 같은 js의 동적 언어로서의 동작원리를 담고 있는 JS 핵심 원리이다.

; 실행 가능한 코드에 제공할 환경정보를 모아놓은 객체

<aside>
🧳 여기서 말하는 **실행 가능한 코드**

---

- 전역 코드: 전역 영역에 존재하는 코드
- Eval 코드: eval 함수로 실행되는 코드
- 함수 코드: 함수 내에 존재하는 코드

일반적으로는 전역 코드와 함수 코드를 말한다.

</aside>

## 실행 컨텍스트의 역할

1. 전체 코드의 환경과 순서를 보장
    
    동일한 환경에 있는 코드를 실행할 때 필요한 환경 정보를 모아 객체를 구성 & 이를 `콜 스택`에 쌓아올림 & 가장 위에 쌓여있는 컨텍스트와 관련 있는 코드를 실행
    
2. 실행 컨텍스트가 활성화되는 시점에 선언된 변수를 hoisting
3. 외부 환경 정보 구성
4. this 값 설정

⇒ 실행 컨텍스트는 JavaScript의 **동적 언어**로서의 성격을 가장 잘 파악할 수 있는 개념

<aside>
🗃️ **`콜 스택Call Stack`**

---

; 자바스크립트 엔진이 원시타입 값과 함수 호출의 실행 컨텍스트를 저장하는 곳

자바스크립트는 단일 스레드 기반 언어.

자바스크립트 엔진이 단일 콜 스택을 가짐 → 요청이 동기적으로 처리됨

</aside>

## 실행 컨텍스트 구성

<aside>
📚 **실행 컨텍스트가 생성되는 경우**

---

다음과 같은 것들을 이용하여 call stack에 실행 컨텍스트가 쌓인다.

- 전역 공간은 자동으로 컨텍스트로 구성
- (일반적)함수 실행
- eval()함수 실행
- block 생성 (ES6+)
</aside>

실행 컨텍스트를 구성할 때 아래와 같은 것들이 생성된다.

### 1. Variable Environment

; 현재 컨텍스트 내 식별자들에 대한 정보 + 외부 환경 정보

- 선언 시점의 Lexical Environment 스냅샷 → 변경 사항 반영 ❌

### 2. Lexical Environment

- (최초)VariableEnvironment를 복사 → 변경 사항이 실시간으로 반영 ⭕️

<aside>
1️⃣ **environmentRecord**

JS 엔진은 코드가 실행되기 전 실행 컨텍스트에 속한 변수명을 모두 알고 있다.

---

: 현재 컨텍스트와 관련된 코드의 식별자 정보(매개변수 식별자, 함수 자체, 함수 내부 식별자) 저장

- **호이스팅 발생**

*`호스트 객체*Host Object*`

: 전역 실행 컨텍스트는 변수 객체를 생성하는 대신 전역 객체를 활용 

ex.브라우저-Window 객체, Node-Global 등

</aside>

<aside>
2️⃣ **outerEnvironmentReference**

---

- outerEnvironmentReference는 현재 호출된 함수가 **선언될 당시**의 LexicalEnvironment를 참조한다.
- **스코프, 스코프 체인 형성**
    
    outerEnvironmentReference 덕분에 스코프 체이닝이 가능하다.
    

*ES5까지는 오직 함수에 의해서만 스코프가 생성

</aside>

### 3. ThisBinding

this 식별자가 바라봐야 할 대상 객체

## 전역 컨텍스트와 함수 컨텍스트

<aside>
🌏 `전역 컨텍스트`

---

; 코드 내부에서 별도의 실행 명령 없이 브라우저에서 자동으로 실행하는 컨텍스트

</aside>

![출처: [https://chanhuiseok.github.io/posts/js-4/#:~:text=변수 객체에는 [[scope,범위를 나타내는 것입니다.&text=함수 안에 정의된 변수,변수 객체에 생성됩니다](https://chanhuiseok.github.io/posts/js-4/#:~:text=%EB%B3%80%EC%88%98%20%EA%B0%9D%EC%B2%B4%EC%97%90%EB%8A%94%20%5B%5Bscope,%EB%B2%94%EC%9C%84%EB%A5%BC%20%EB%82%98%ED%83%80%EB%82%B4%EB%8A%94%20%EA%B2%83%EC%9E%85%EB%8B%88%EB%8B%A4.&text=%ED%95%A8%EC%88%98%20%EC%95%88%EC%97%90%20%EC%A0%95%EC%9D%98%EB%90%9C%20%EB%B3%80%EC%88%98,%EB%B3%80%EC%88%98%20%EA%B0%9D%EC%B2%B4%EC%97%90%20%EC%83%9D%EC%84%B1%EB%90%A9%EB%8B%88%EB%8B%A4).](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eaae050e-2a55-4a33-ad79-e75ce2d96a77/Untitled.png)

출처: [https://chanhuiseok.github.io/posts/js-4/#:~:text=변수 객체에는 [[scope,범위를 나타내는 것입니다.&text=함수 안에 정의된 변수,변수 객체에 생성됩니다](https://chanhuiseok.github.io/posts/js-4/#:~:text=%EB%B3%80%EC%88%98%20%EA%B0%9D%EC%B2%B4%EC%97%90%EB%8A%94%20%5B%5Bscope,%EB%B2%94%EC%9C%84%EB%A5%BC%20%EB%82%98%ED%83%80%EB%82%B4%EB%8A%94%20%EA%B2%83%EC%9E%85%EB%8B%88%EB%8B%A4.&text=%ED%95%A8%EC%88%98%20%EC%95%88%EC%97%90%20%EC%A0%95%EC%9D%98%EB%90%9C%20%EB%B3%80%EC%88%98,%EB%B3%80%EC%88%98%20%EA%B0%9D%EC%B2%B4%EC%97%90%20%EC%83%9D%EC%84%B1%EB%90%A9%EB%8B%88%EB%8B%A4).

1. `전역 컨텍스트`가 먼저 생성된다.
2. `함수 실행 컨텍스트`: 함수 호출 시마다 컨텍스트가 발생한다.
3. 컨텍스트 생성 시, 컨텍스트 안에 1)변수 객체*Variable object* 2)scope chain 3)this 생성
    
    변수 객체에는 arguments, variable이 있다.
    
4. 컨텍스트 생성 후 함수가 실행된다.
    
    사용되는 변수들은 변수 객체 안에서 값을 찾고, 없으면 스코프 체인을 따라 올라가며 찾는다.
    
5. 함수 실행이 마무리 되면 해당 컨텍스트는 사라진다.(클로저 제외)
6. 페이지가 종료되면 전역 컨텍스트가 사라진다.

<aside>
🚘 **전역 컨텍스트 관련 코드를 진행하다가 `outer()` 호출 시 발생하는 일**

---

[https://pottatt0.tistory.com/m/entry/한-번에-모아보는-프론트엔드-면접-질문-JavaScript](https://pottatt0.tistory.com/m/entry/%ED%95%9C-%EB%B2%88%EC%97%90-%EB%AA%A8%EC%95%84%EB%B3%B4%EB%8A%94-%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-JavaScript)

콜 스택에서 전역 컨텍스트 관련 코드를 순차 진행 → outer() 호출

1. JavaScript 엔진이 outer에 대한 환경 정보 수집 후 outer 실행 컨텍스트 생성 
2. outer 실행 컨텍스트를 콜 스택 맨 위에 저장
3. 전역 컨텍스트와 관련된 코드 일시 중단
4. outer 실행 컨텍스트와 관련된 코드(즉, outer 함수 내부의 코드)를 순차로 실행
</aside>

### **실행 컨텍스트의 객체에 담긴 정보**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/95a44e9f-2925-4257-97aa-f49003e54102/Untitled.png)

1. **변수객체*Variable Object*(=VO)**
    
    코드가 실행될 때 JS 엔진에 의해 참조. 코드에서 접근 불가
    
    - 변수
        - 실행 되기 전까지 생성 ⭕️ 초기화❌ → undefined
    - 매개변수parameter와 인수 정보arguments
    - 함수 선언(함수 표현식은 ❌)
        - 함수 선언식과 함수 표현식의 차이
            
            ```cpp
            function foo() {} // 함수 선언식
            var bar = function () {} // 함수 표현식
            ```
            
        - 함수 표현식으로 생성된 함수 생성 ⭕️ 초기화 ❌ → undefined

1. **Scope Chain**
    
    ![출처: [https://chanhuiseok.github.io/posts/js-4/](https://chanhuiseok.github.io/posts/js-4/)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/29b13d88-28bc-4634-b66c-4f79aa3182c3/Untitled.png)
    
    출처: [https://chanhuiseok.github.io/posts/js-4/](https://chanhuiseok.github.io/posts/js-4/)
    
    ; 연결리스트 형태의 스코프 정보
    
    *Scope: 현재 실행 중인 컨텍스트의 유효한 범위를 나타내는 것
    

1. **thisValue**
    
    이 변수 객체의 this에 바인딩할 객체
    
    - (함수 호출 방식에 따라 달라지는 this 바인딩 제외)기본적으로 전역 객체에 바인딩

<aside>
💘 **일반 함수 `function () {}`과 화살표 함수`const = () ⇒ {}`의 차이**

---

일반 함수는 자체적으로 this 할당

but 화살표 함수는 자체적으로 this ❌ → 부모 스코프의 this 참조: 정적 컨텍스트를 가진다.

*정적 컨텍스트*Lexical Context*는 소스코드가 작성된 그 문맥의 실행 컨텍스트나 호출 컨텍스트에 의해 결정된다. 즉, 함수가 실행된 위치 ❌, 정의된 위치에서의 컨텍스트를 참조한다.

</aside>

# 참고 자료

[Front-End 면접 질문 대비 Part4(SSR, CSR, Execution Context, Iterator, Event Delegation)](https://velog.io/@holim0/Front-End-면접-질문-대비-Part4#실행-컨텍스트)

[[기술면접] js 실행컨텍스트](https://velog.io/@win/기술면접-js-실행컨텍스트)

[[ 한 번에 모아보는 프론트엔드 면접 질문 ] JavaScript](https://pottatt0.tistory.com/m/entry/한-번에-모아보는-프론트엔드-면접-질문-JavaScript)

[11. 기술면접 - 자바스크립트 - this](https://theheydaze.tistory.com/626)

[자바스크립트 실행 컨텍스트 | 개발자 황준일](https://junilhwang.github.io/TIL/Javascript/Domain/Execution-Context/#_1-개념)

[JavaScript - 자바스크립트 실행 컨텍스트, 스코프(Scope), 스코프 체인](https://chanhuiseok.github.io/posts/js-4/)
