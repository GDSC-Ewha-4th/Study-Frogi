정리 노션 링크입니다: https://boom-passbook-4e2.notion.site/ES6-1d1e8a9d43c94032b4c061c6c6b868cf

<aside>
1️⃣ **ES6에서 추가된 것을 아는대로 말해보세요.**

---

- 답변
    
    ES6에는 화살표 함수와 Rest 파라미터, 그리고 let과 const 키워드가 도입되었습니다.
    
    화살표 함수는 자체적으로 this 바인딩을 갖지 않기 때문에, 콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결하기 위한 대안책으로 유용하게 사용할 수 있습니다.
    
    그리고 Rest 파라미터는 함수 정의 시 매개변수 개수를 정의할 수 없는 가변 인자 함수의 인수 목록을 배열로 전달받을 수 있는 파라미터인데요, 이 덕분에 기존에 가변 인자 함수의 인수 목록에 배열 메소드를 쓰기 위해 arguments라는 유사 배열 객체에 인수를 담고 그것을 배열로 변환해야하는 불편함을 감소할 수 있습니다.
    
    let과 const는 함수 레벨 스코프를 따라 의도와 다르게 동작할 위험이 있는 var를 대체할 수 있는, 블록 스코프를 가진 변수 선언 키워드입니다.
    
</aside>

<aside>
2️⃣ 일반 함수와 화살표 함수의 차이를 설명해주세요

---

- 답변
    
    첫 번째로 일반 함수는 생성자로 호출할 수 있지만 화살표 함수는 그렇지 않다는 점입니다. 그래서 화살표 함수는 프로토타입 프로퍼티도 가지지 않고, 프로토타입을 생성하지도 않습니다.
    
    또한 일반 함수가 super를 제외한 this, arguments, new.target을 가지는 데에 반해, 화살표 함수는 자체적인 this, arguments, super, new.target 을 모두 갖지 않고, 스코프 체인을 통해 상위 스코프를 참조합니다. 
    
    마지막으로 화살표 함수는 strict 모드가 아닌 일반 함수와 달리 매개변수 이름을 중복하여 선언할 수 없다는 차이가 있습니다.
    
</aside>

<aside>
3️⃣ **var, let, const의 차이점을 설명해주세요.**

---

- 답변
    
    var은 함수 레벨 스코프를 지원합니다. let과 const는 블록 스코프를 가지고 공통적으로 재선언이 되지 않습니다. 하지만 let는 재할당이 가능하고, const는 선언과 동시에 할당이 되기에 재할당은 불가능합니다.
    
</aside>

## 학습 내용

> 이처럼 ES6 이전의 함수는 사용 목적에 따라 명확히 구분되지 않는다.
> 
> 
> ES6 이전의 모든 함수는 callback이면서 constructor다.
> 
> -모던 자바스크립트 DeepDive p.469
> 
> ```c
> var foo = function () {};
> 
> foo(); // -> undefined
> new foo(); // -> foo {}
> ```
> 

> 
> 
> 
> 위 예제와 같이 객체에 바인딩된 함수를 생성자 함수로 호출하는 경우가 흔치는 않겠지만 문법상 가능하다는 것은 문제가 있다. 그리고 이는 성능 면에서도 문제가 있다. 객체에 바인딩된 함수가 constructor 라는 것은 객체에 바인딩된 함수가 prototype 프로퍼티를 가지며, 프로토타입 객체도 생성한다는 것을 의미하기 때문 이다.
> 함수에 전달되어 보조 함수의 역할을 수행하는 콜백 함수도 마찬가지다. 콜백 함수도 constructor 이기 때문에 불필요한 프로토타입 객체를 생성한다.
> 
> -모던 자바스크립트 DeepDive p.470
> 

## 화살표 함수

| ES6 함수의 구분 | constructor | prototype | super | arguments |
| --- | --- | --- | --- | --- |
| 일반 함수(Normal) | ⭕️ | ⭕️ | ❌ | ⭕️ |
| 메서드(Method) | ❌ | ❌ | ⭕️ | ⭕️ |
| 화살표 함수(Arrow) | ❌ | ❌ | ❌ | ❌ |

일반 함수: 함수 선언문 or 함수 표현식으로 정의한 함수

일반 함수는 ES6 이전의 함수와 동일

but 일반 함수는 constructor 이지만 화살표 함수는 non-constructor이다. 

## 메서드

이전까지는 메서드에 대한 명확한 정의가 없었으나

ES6를 기점으로 메서드는 메서드는

- 축약 표현으로 정의된 함수만을 의미한다.
    
    ```jsx
    const obj = {
    	x: 1,
    	foo() {return this.x;}, // foo는 메서드다
    	bar: function() {return this.x; } // bar에 바인딩된 함수는 메서드 X 일반 함수 O
    };
    ```
    
- 인스턴스를 생성할 수 없는 non-constructor다.
    
    → prototype 프로퍼티가 없다
    
    → 프로토타입 생성 X
    
- 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖는다.
    
    → super 키워드 사용 가능
    
    $\because$ super는 [[HomeObject]] 를 사용하여 수퍼 클래스의 메서드를 참조
    
    $\therefore$ ES6 메서드가 아닌 함수는 super 키워드 사용 불가(내부 슬롯 [[HomeObject]]를 갖지 않아서) 
    
    <aside>
    📌 그러니 메서드를 정의할 때 프로퍼티 값으로 익명 함수 표현식을 할당하는 ES6 이전 방식은 지양하자.
    
    </aside>
    

## 화살표 함수

화살표 함수는 콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결하기 위한 대안으로 유용하다.

### 화살표 함수와 일반 함수의 차이

- 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor이다.
    
    → prototype 프로퍼티도 없고 프로토타입도 생성하지 않는다.
    
- 중복된 매개변수 이름을 선언할 수 없다.
    
    *일반 함수는 중복된 매개변수 이름을 선언해도 OK
    
    ```jsx
    function normal(a,a){return a+a;}
    console.log(normal(1,2)); // 4
    ```
    
    단, strict mode에서 중복된 매개변수 이름을 선언하면 에러 발생
    
- 화살표 함수는 함수 자체의 this, arguments, super, new.target 바인딩을 같지 않는다.
    
    화살표 함수 내부에서 this, arguments, super, new.target을 참조하면 스코프 체인을 통해 상위 스코프의 this, arguments, super, new.target을 참조한다.
    
    화살표 함수와 화살표 함수가 중첩된 경우 → 가장 가까운 함수 중에서 화살표 함수가 아닌 함수의 this, arguments, super, new.target 참조
    

화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 this 를 참조하면 상위 스코프의 this 를 그대로 참조한다. 이를 lexical this라 한다. 이는 마치 렉시컬 스코프 5 와 같이 화살표 함수의 this 가 함수가 정의된 위치에 의해 결정된다는 것을 의미한다. p.480

```jsx
// increase 프로퍼티에 할당한 화살표 함수의 상위 스코프는 전역이다.
// 따라서 increase 프로퍼티에 할당한 화살표 함수의 this는 전역 객체를 가리킨다.

const counter = { 
	num: 1 ,
	increase: () => ++this . num 
};

console . log(counter . increase()); // NaN
```

화살표 함수는 함수 자체의 this 바인딩을 갖지 않기 때문에 [Function.prototype.call/apply/bind](http://Function.prototype.call/apply/bind) 메서드를 사용해도 화살표 함수 내부의 this 를 교체할 수 없다. p.482

메서드를 화살표 함수로 정의하는 것은 피해야 한다. p.482

프로퍼티를 동적 추가할 때는 ES6 메서드 정의를 사용할 수 없으므로 일반 함수를 할당한다. 

클래스 필드에 할당한 화살표 함수는 프로토타입 메서드가 아닌 인스턴스 메서드가 된다. 메서드를 정의할 때는 ES6 메서드 축약 표현으로 정의한 ES6 메서드를 사용하는 것이 좋다. 

```jsx
// Good
class Person {
	// 클래스 필드 정의
	name = 'Lee';
	sayHi(){console.log(`Hi ${this.name}`);}
}
const person = new Person();
person.sayHi(); // Hi Lee
```

### super

화살표 함수는 함수 자체의 super ❌ 상위 스코프의 super 참조 ⭕️

*super: 내부 슬롯 [[HomeObject]]를 갖는 ES6 메서드 내에서만 사용 가능

### arguments

화살표 함수는 함수 자체의 arguments 바인딩 갖지 ❌ 상위 스코프의 arguments를 참조

## Rest 파라미터

<aside>
📌 **Rest 파라미터의 필요성**

---

화살표 함수에서는 arguments 객체 사용 불가.

상위 스코프의 arguments 객체를 사용할 수는 있지만 화살표 함수 자신에게 전달된 인수 목록 확인 불가 등의 & 상위 함수에 전달된 인수 목록 확인 → 도움 안됨

</aside>

- 함수에 전달된 인수들의 목록을 배열로 전달받음

### arguments

ES5: 함수 정의 시 매개변수 개수를 확정할 수 없는 가변 인자 함수의 경우 arguments 객체를 활용하여 인수 전달 받음

<aside>
🤔 arguments 객체

---

- 함수 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체
    
    → 배열 메서드를 사용하려면 call이나 apply를 이용해 배열로 먼저 변환해야함
    
- 함수 내부에서 지역변수처럼 사용 가능
</aside>

ES6: 가변 인자 함수의 인수 목록을 배열로 직접 전달 받음 → arguments 객체를 배열로 변환하는 번거로움 회피 가능

- 함수와 ES6 메서드는 원래 Rest 파라미터와 arguments 객체 모두 사용 가능
    
    but 화살표 함수는 자체 arguments가 없으므로 반드시 rest 파라미터 사용해야한다.
    

## 매개변수 기본값

JS 엔진은 매개변수의 개수와 인수의 개수를 체크 ❌ → 인수가 전달되지 않은 매개변수의 값은 undefined

⇒ 기본값 필요 as 방어코드

- 인수를 전달하지 않은 경우와 undefined를 전달한 경우에만 유효
- rest 파라미터에는 기본값을 지정할 수 없다.
- 함수 정의 시 선언한 매개변수의 개수를 나타내는 함수 객체의 length 프로퍼티와 arguments 객체에 아무런 영향 주지 ❌
    
    ```jsx
    function sum(x,y=0){
    	console.log(arguments);
    }
    
    console.log(sum.length); // 1
    
    sum(1); // Arguemnts {'0':1}
    sum(1,2); // Arguments {'0':1, '1':2}
    ```
    

## 참고 자료

모던 자바스크립트 DeepDive
