정리한 블로그 글입니다. https://velog.io/@kados22/FE-기술-면접-JS-비동기-처리에-대해-설명해주세요

![글 표지_제목은 async/await 부제목은 모던자바스크립트 Deepdive 분류는 FE 면접 준비](https://velog.velcdn.com/images/kados22/post/cdfebb11-769d-48e2-bd5a-d663acbd348c/image.png)


> **1️⃣ 비동기 함수에 대해 설명해주세요.**
비동기 함수란 함수의 실행 결과가 즉시 반환되지 않고, 특정 조건이 충족될 때까지 기다리는 함수입니다. 비동기 함수는 일반적으로 콜백 함수나 Promise 객체를 반환하는데요, 콜백 함수는 비동기 작업이 완료되었을 때 호출되고, Promise 객체는 비동기 작업이 성공했는지 혹은 실패했는지를 나타냅니다. 
비동기 함수를 잘 사용하면 서비스의 성능과 반응성을 잘 유지할 수 있으나, 콜백 지옥이 발생할 수 있으므로 Promise의 후속 처리 메서드(then, catch, finally)나 async, await를 이용하여 적절하게 코드를 구성하는 것이 필요합니다.
여러개의 비동기 함수가 실행되면 이벤트 루프는 비동기 함수 호출을 처리하고, 비동기 함수가 완료되었을 때 콜백 함수를 호출합니다. 이벤트 루프는 실행 대기 중인 비동기 함수가 있으면 해당 함수를 호출하고, 실행이 완료될 때까지 다음 비동기 함수를 호출합니다. 즉, 여러 개의 비동기 함수가 실행될 때 이 함수는 동시에 실행되며, 이벤트 루프에 의해 비동기 함수의 실행순서가 제어된다고 할 수 있습니다.


> 2️⃣ **이벤트 루프란 무엇인가요?**
여러 비동기 함수가 실행되면, 브라우저와 싱글 스레드 방식으로 동작하는 자바스크립트 엔진이 함께 처리합니다. 여기서 이벤트 루프는 실행 컨텍스트가 생기고 없어지는 JS 엔진의 콜스택과 비동기 함수의 콜백 함수나 이벤트 핸들러가 일시적으로 보관되는 브라우저의 태스크 큐를 반복적으로 확인하여 콜 스택이 모두 비어있으면 태스크 큐에 대기 중인 함수를 선입선출 방식으로 콜 스택으로 이동시키는 역할을 하는 브라우저 내장 기능입니다.


> 3️⃣ **async, await 사용 방법을 설명해주세요.**
async/await는 ES8부터 도입되어 Promise를 기반으로 하는 비동기 처리 문법으로, 동기적인 것처럼, 가독성 좋게 비동기 처리가 가능하다는 장점이 있습니다. 함수 앞머리에 async 키워드를 써서 async 함수로 정의하고, 함수 내부에서 프로미스를 반환하는 부분 앞에 await 키워드를 사용하면 async/await를 사용할 수 있는데요, 내부 코드를 진행하다 await 키워드를 마주하면 비동기적으로 처리되는 작업이 완료될 때까지 기다렸다가 결과값을 받아 처리할 수 있고, 최종적으로는 항상 Promise 객체를 반환한다는 특징이 있습니다. 

> 4️⃣ **promise와 async/await의 차이점을 설명해주세요
Promise를 사용한 비동기 통신과 async, await를 사용한 비동기 통신의 차이를 설명해주세요.**
첫 번째로는 async/await 문에서는 try...catch문으로 에러 처리가 가능하지만 Promise문은 그렇지 않다는 점입니다. 프로미스를 반환하는 비동기 함수는 명시적으로 호출이 가능해서, 호출자가 명확하기 때문에 try catch 문으로 에러를 처리할 수 있기 때문에 이것이 가능합니다. 또한, 최종적으로 catch 문에서 에러를 출력하는 Promise와 달리 쉽게 문제가 발생한 부분을 찾을 수 있다는 장점도 있습니다.
두번째는 코드 가독성 입니다. Promise는 과한 프로미스 체이닝으로 가독성이 떨어질 수 있지만 async/await는 그럴 가능성이 적고, 동기적인 순서로 코드를 쉽게 파악할 수 있습니다.


---
아래는 모던 자바스크립트 Deepdive를 읽고 정리한 내용입니다!

## 학습 내용
> 📌 **자바스크립트의 특징**
	- JS 엔진은 단 하나의 실행 컨텍스트 스택(=콜 스택)을 갖는다.
	- JS 엔진은 싱글 스레드 방식으로 동작한다.
    *`싱글 스레드single thread`란? 
    한 번에 하나의 task만 실행가능한 방식이다.
    ‼️ 하지만, 브라우저는 멀티 스레드로 동작한다 ‼️

### 동기_synchronous_와 비동기_asynchronous_
- `동기`; 현재 실행 중인 task가 종료할 때까지 다음에 실행될 task가 대기하는 방식
- `비동기`; 현재 실행중인 task가 종료 되지 않은 상태라 해도 다음 task를 곧바로 실행하는 방식
	- ex. `setTimeout`, `setInterval`, HTTP 요청, 이벤트 핸들러

|    |장점 |단점
|----|:----:|:----:
|동기|실행 순서 보장   |  블로킹 ⭕️
|비동기|블로킹 ❌   |  실행 순서 미보장 

*`블로킹blocking`이란? 먼저 호출된 함수가 실행 종료될 때까지 다음 함수의 작업이 중단되는 현상

### 이벤트 루프와 태스크 큐
> 이벤트 루프event loop 덕분에 
많은 task가 동시에 처리되는 것처럼 보인다!(자바스크립트의 동시성)

![이벤트 루프와 브라우저 환경 구조 사진. 출처는 모던자바스크립트DeepDive](https://velog.velcdn.com/images/kados22/post/fd6caaec-bf3f-4967-90e1-bc1996b1ca1d/image.png)	

브라우저와 자바스크립트 엔진이 협력하여 비동기 함수를 실행한다.

- 콜스택: 실행 컨텍스트가 추가되고 제거되는 스택 자료구조
- 힙:객체가 저장되는 메모리 공간.
	- 실행 컨텍스트가 참조한다.
    - 크기가 런타임에 동적 할당되므로 구조화 되어 있지 않다.
- 태스크 큐: 비동기 함수의 콜백 함수 or 이벤트 핸들러가 일시적으로 보관되는 영역
- 이벤트 루프
	- 콜 스택과 태스크 큐를 반복 확인 ➡️ 태스크 큐에 대기 중인 함수를 FIFO 방식으로 콜 스택에 이동시킨다.
    *콜백 함수를 태스크 큐에 푸시하는 건 브라우저가 한다!
  

    
>🧪 **코드로 확인해보자!**
둘 중에 먼저 실행되는 함수는?
```javascript
function foo(){
	console.log('foo');
}
function bar(){
	console.log('bar');
}
setTimeout(foo,0); // 0초(실제는 4ms) 후에 foo 함수 호출
bar;
```
---
bar 함수가 먼저 실행된다.
1. setTimeout 함수 실행(콜백 함수 호출 스케줄링)
2. (설정 타이머 만료 시)콜백 함수 foo가 태스크 큐로 푸시 후 대기
3. bar 함수 실행
4. 전역 코드 실행
5. (콜 스택이 모두 비었다면)foo 함수 실행
(출처: 모던자바스크립트DeepDive p.814)

### 제너레이터
; (ES6) 코드 블록의 실행을 일시 중지 했다가 필요한 시점에 재개할 수 있는 함수

> 📌 제너레이터와 일반 함수의 차이
> 1. 함수 실행 제어권
	- 일반 함수: 함수 독점 
    - 제너레이터: 양도_yield_ 가능(함수 호출자)
    즉, 제너레이터 함수를 사용하면 함수 호출자가 함수 실행을 일시 중지/재개 할 수 있다.
    2. 함수 상태 전달 방향
    - 일반 함수: 실행 중 상태 변경 불가
    - 제너레이터: 양방향(함수 호출자에게 상태를 줄 수도, 받을 수도 있다.)
	3. 반환 값
    - 일반 함수: 코드 실행 후 값 반환
    - 제너레이터: 이터러블이자 이터레이터인 제너레이터 객체 반환(함수 코드 실행❌)
    
- 제너레이터 객체는
	이터러블 = Symbol.iterator 메서드 상속
    이터레이터 = value, done 프로퍼티 가짐, next 메서드 소유
- `next()`를 호출하면 yield 표현식까지 실행되고 일시 중지 된다. 이때 함수의 제어권이 호출자로 양도yield 된다. 또다시 `next()`를 호출하면 다음 yield 표현식까지 실행된다.
- 제너레이터를 이용하면 then/catch/finally 없이 비동기 처리 결과를 반환하도록 구현할 수 있다.[모던자바스크립트DeepDive 예제 46-12 참조]

### async와 await
> 제너레이터를 이용한 비동기 처리는 코드가 무척 장황하다!
➡️ ES8부터 async/await 도입
➡️ then/catch/finally 없이 동기 처리처럼 프로미스 사용 🆗

```javascript
// 모던자바스크립트 DeepDive 예제 46-19 p.883
async function foo() {
	const res = await Promise.all([
    	new Promise(resolve => setTimeout(()=> resolve(1),3000));
    	new Promise(resolve => setTimeout(()=> resolve(2),2000));
  		new Promise(resolve => setTimeout(()=> resolve(3),1000));
    ]);
  
  	console.log(res); // [1,2,3]
}

foo(); // 약 3초 소요
```

```javascript
// 모던자바스크립트 DeepDive 예제 46-20 p.883
async function bar(n){
	const a = await new Promise(resolve => setTimeout(()=>resolve(n),3000));
  	// 비동기 처리를 수행하려면 앞 비동기 처리 결과가 필요하다.
  	const b = await new Promise(resolve => setTimeout(()=>resolve(a+1),2000));
  	const c = await new Promise(resolve => setTimeout(()=>resolve(b+1),1000));
  
  console.log([a,b,c]); //[1,2,3]
}

bar(1); // 약 6초 소요된다.
```

- async 함수는 언제나 프로미스를 반환한다. 프로미스가 아닌 반환 값은 암묵적으로 resolve하여 프로미스 형태로 반환한다.
- await 키워드는 반드시 프로미스 앞에서 사용해야 한다.

> 📌 async/await에서의 에러 처리
- try...catch 문 사용 🆗
프로미스를 반환하는 비동기 함수는 명시적으로 호출할 수 있기 때문에 호출자가 명확하기 때문이다.
(원래)비동기 함수의 콜백 함수 호출 주체 != 비동기 함수 ➡️ try...catch 문으로 에러 캐치 ❌
- 네트워크 에러 캐치 🆗
- 함수 내에서 처리되지 않은 에러는 reject되어 프로미스로 반환


## 새롭게 알게된 점
> ⏰ **setTimeout이 의도한 간격의 지연 호출을 보장하지 않는 이유는?**
지연 시간 이후에 콜백 함수가 태스크 큐에 푸시되어 대기하게 되지만, 콜 스택이 비어야 호출되므로 약간의 시간차가 발생할 수 있기 때문이다. 


## 참고 자료
- 모던 자바스크립트 DeepDive Ch.42 비동기 프로그래밍
- 모던 자바스크립트 DeepDive Ch.46 제너레이터와 async/await
- [현직 개발자가 정리해주는 프론트엔드 신입 기술 면접 문제 은행 20선(feat. 전 카카오 엔터프라이즈 개발자)](https://zero-base.co.kr/event/media_insight_contents_FE_frontend_tech_Interview?gclid=CjwKCAjwq-WgBhBMEiwAzKSH6I1sjO48HgyT_mJAdrIbwTmsfx3DRpQjvvBtprvi8B-GNhmyBmryGhoC6WMQAvD_BwE)
- [Promise와 async/await 차이점](https://velog.io/@pilyeooong/Promise%EC%99%80-asyncawait-%EC%B0%A8%EC%9D%B4%EC%A0%90)
- [promise와 async await의 차이점](https://mong-blog.tistory.com/entry/promise%EC%99%80-async-await%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
