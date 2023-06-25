정리된 [노션 바로가기](https://boom-passbook-4e2.notion.site/Promise-9d433d278f084b69951c42ed3350fe86?pvs=4)입니다. 

<aside>
1️⃣ **콜백 지옥(Callback hell)을 해결하는 방법을 말씀해주세요.**

---

- 대답
    
    콜백 지옥이란 콜백 함수가 중첩되어 그 복잡도가 높아지는 현상을 말하는데요, 
    
    일반적으로 이 콜백 지옥을 해결하기 위해서는 ES6부터 추가된 Promise를 사용합니다. Promise는 인수로 콜백함수를 전달받고 이 속에서 비동기처리를 수행합니다. 이때 비동기 처리가 성공하면 콜백함수의 인수로 전달받은 resolve를, 실패하면 reject 함수를 호출하고, 후속 처리 메소드를 통한 에러 처리도 가능합니다.
    
    또한 가독성을 위해 Promise와 함께 ES2017에 추가된 async, await를 함께 사용하기도 합니다.
    
</aside>

<aside>
2️⃣ **Promise와 Callback 차이를 설명해주세요.**

---

- 대답
    
    Callback 함수는 내부의 비동기로 동작하는 코드 완료를 기다리지 않고 종료되어 로직 바깥에서는 결과 값을 사용할 수가 없는 등 의도대로 동작하지 않는 부분이 있습니다. 하지만 Promise는 비동기 로직에서 처리된 결과값이 Promise 객체에 저장되기 때문에 로직 밖에서도 사용이 가능합니다.
    
    또한 Callback 함수는 비동기의 결과를 이용하기 위해서라면 함수 내부에서 중첩 호출되어야 하므로 가독성이 떨어지지만 Promise 함수는 정적 메서드를 통해 가독성을 높일 수 있습니다.
    
</aside>

<aside>
3️⃣ **다음 함수를 실행 했을 때 콘솔에 출력되는 결과는?**

```jsx
var func = () => {
	for(var i=0; i<3; i++){
		setTimeout(()=>{
			console.log(i);
		}, 1000*i);
	}
}
func();
```

문제 출처: https://jongbeom-dev.tistory.com/118

---

- 대답
    
    ```jsx
    3
    3
    3
    ```
    
    setTimeout 함수를 호출하면 콜백 함수를 호출 스케줄링한 다음 즉시 종료됩니다. 즉, setTimeout 함수의 콜백 함수는 setTimeout 함수가 종료된 이후에 호출이 되므로 이미 i가 3까지 모두 증가한 상태에서 console을 호출하여 3이 3번 출력됩니다.
    
</aside>

## 학습 내용

<aside>
📌 (ES6) **Promise 등장 배경**

---

비동기 처리를 위한 기존 콜백 패턴의 단점

1. 콜백 헬
    
    → 실수 유발, 가독성 저하
    
2. 에러 처리 곤란
</aside>

## 콜백 헬

; 콜백 함수를 통해 비동기 처리 결과에 대한 후속 처리를 수행하는 비동기 함수가 비동기 처리 결과를 가지고 또다시 비동기 함수를 호출해야 한다면 콜백 함수 호출이 중첩되어 복잡도가 높아지는 현상

### 의도대로 동작하지 않는 비동기 함수

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6086b36f-5f10-47a2-990a-6e0ba52d03ef/Untitled.png)

**[ setTimeout() ]**

<aside>
📌 **setTimeout 함수가 비동기 함수인 이유**

---

![p.843](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3bc4e262-7aa6-4f56-85bd-0b689167d5c0/Untitled.png)

p.843

</aside>

![p.843](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44e20a0c-a92d-4897-8ecc-aece83d18535/Untitled.png)

p.843

**[ get() ]**

<aside>
📌 **get 함수가 비동기 함수인 이유**

---

get 함수 내부의 onload 이벤트 핸들러가 비동기로 동작하기 때문이다.

![p.846](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/98fa2839-48f9-413e-9a66-af5906fb167c/Untitled.png)

p.846

</aside>

➡️

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e839d6ff-01bc-4931-94b8-eb684d59a80d/Untitled.png)

## Promise

; 비동기 처리 상태와 처리 결과를  관리하는 객체

- (1) 비동기 처리가 어떻게 진행되는지를 나타내는 상태 정보와
(2) 비동기 처리 결과를 갖는다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2dd03ab6-c7cf-4986-b514-dc8e70b73186/Untitled.png)

- `settled` 상태: fulfilled 또는 rejected 상태와 관계 없이 pending이 아닌 상태. 비동기 처리가 수행된 상태.

## Promise의 후속 처리 메소드

- 모든 후속 처리 메서드는 프로미스를 반환하며, 비동기로 동작한다.

### then

### catch

### finally

## Promise의 에러 처리

: `then`의 두 번째 콜백 함수 or `catch`

<aside>
📌 **catch 메서드 사용을 더 권장한다**

---

- `then` 메서드의 두 번째 콜백 함수는 첫 번째 콜백 함수에서 발생한 에러 캐치 불가
- 코드가 복잡 → 가독성 저하
- `catch` 메서드를 모든 `then` 메서드 호출 이후에 호출 시,
    
    비동기 처리에서 발생한 에러(`rejected`) 뿐만 아니라 `then` 메서드 내부에서 발생한 에러까지 모두 캐치 가능
    
</aside>

## Promise Chaining

; 프로미스를 연속적으로 호출

- try, catch, finally 후속 처리 메서드는 언제나 프로미스를 반환하므로 가능

![p.857](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b554d81c-0e08-4ac6-abe8-57ee1b162fb6/Untitled.png)

p.857

## 프로미스의 정적 메서드

### Promise.all

![p.860](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ce317054-8d6f-4ef6-a8d4-370dbc84fa50/Untitled.png)

p.860

- 첫 번째 Promise가 resolve한 처리 결과부터 차례대로 배열에 저장해 그 배열을 resolve하는 새로운 프로미스 반환
    
    ⇒ 처리 순서가 보장된다.
    
- 배열의 프로미스가 하나라도 rejected 상태가 되면 나머지 프로미스가 fulfilled 상태가 되는 것을 기다리지 않고 즉시 종료 & 에러 반환한다.

## 마이크로태스크 큐

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db3af66a-b6c5-4035-b080-7ae98a789bc2/Untitled.png)

## fetch

![p.866](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/03873ace-3cde-441e-9dd8-afeb924663cc/Untitled.png)

p.866

![p.867](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/34f56800-41e8-4257-a862-7859b8ec1e64/Untitled.png)

p.867

- `axios`는 모든 HTTP 에러를 reject하는 프로미스 반환
    
    ⇒ 모든 에러를 catch에서 처리할 수 있어서 편리
    

## 참고 자료

[[JS] 비동기 처리의 시작 콜백, 그리고 콜백 지옥](https://taesung1993.tistory.com/96)

[[JS] 콜백함수, 콜백지옥](https://yeon-code.tistory.com/102)

[[기술면접] 비동기 호출 callback, promise, async/await의 특징과 차이점](https://velog.io/@ahsy92/기술면접-비동기-호출-callback-promise-asyncawait의-특징과-차이점)

[기술문제 면접(promise(프로미스)의 개념에 대해서 설명하고, 콜백 함수 방식과 차이점을 설명해주세요.)](https://velog.io/@solimlee/기술문제-면접promise프로미스의-개념에-대해서-설명하고-콜백-함수-방식과-차이점을-설명해주세요)
