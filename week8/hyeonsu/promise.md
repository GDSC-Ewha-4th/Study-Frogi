내용이 정리된 노션 링크입니다.
https://www.notion.so/2023-06-26-Promise-e7fa0349bd9a44a2a1b115de0e22aaa5

2023.06.26 [Promise]

<aside>
1️⃣ **콜백 지옥(Callback hell)이 발생하는 원인과 이를 해결하는 방법을 말씀해주세요.**
자바스크립트는 비동기 처리를 위한 하나의 패턴으로 콜백 함수를 사용하지만, 기존 콜백 패턴의 경우 콜백 헬로 인해 가독성이 나빠질 뿐더러 에러 처리가 곤란하고 여러 비동기 처리를 한 번에 처리하는 데도 한계가 있습니다. 콜백 지옥은 비동기 함수 내부의 비동기로 동작하는 코드가 비동기 함수가 종료된 이후에 완료되기 때문에 비동기로 동작하는 코드에서 처리 결과를 외부로 반환하거나 상위 스코프의 변수에 할당하지 못해 후속 처리를 비동기 함수 내부에서 해야 해 발생합니다. 즉 비동기 함수에 비동기 처리 결과에 대한 후속 처리를 수행하는 콜백 함수를 전달해야 하는데, 이때 후속 처리 비동기 함수가 비동기 처리 결과를 가지고 또다시 비동기 함수를 호출해야 하면 콜백 함수 호출이 중첩되어 콜백 헬이 발생합니다. 이러한 전통적인 콜백 패턴은 에러 처리가 곤란하다는 한계도 가지고 있습니다. 에러는 호출자 방향으로 전파되는데 비동기함수는 호출 이후 즉시 콜스택에서 제거되어 비동기 처리 함수가 호출되었을 때 콜스택에 부재하기 때문입니다. 이를 해결하기 위한 방법이 promise 입니다. 프로미스는 비동기 처리를 수행할 콜백 함수를 인수로 전달받는데 이 콜백 함수는 resolve 와 reject 함수를 인수로 전달 받습니다. 그리고 콜백 함수 내에서 비동기 처리를 하게 됩니다.

</aside>

<aside>
2️⃣ **Promise와 Callback 차이를 설명해주세요.**
Promise 는 프로미스의 상태와 프로미스의 결과값을 같이 반환한다는 점에서 콜백과 차이가 있습니다. 프로미스는 3가지 상태 정보를 가집니다. 프로미스가 생성된 직후 기본 상태를 의미하는 pending, resolve 함수를 호출한 상태인 fulfilled, reject 함수를 호출한 상태인 rejected 가 있습니다. 만약 비동기 처리가 성공하면 resolve 함수를 호출하여 프로미스를 fulfilled 상태로 변경하고 비동기 처리에 실패할 경우 reject 함수를 호출하여 프로미스를 rejected 상태로 변경합니다. 아울러 프로미스는 비동기 처리 결과도 상태로 갖습니다. 즉 프로미스는 비동기 처리 상태와 처리 결과를 관리하는 객체라 할 수 있습니다. 프로미스는 비동기 처리에 대한 후속 처리로 세 가지 후속 처리 메서드를 가집니다. then, catch, finally 가 그 세 가지입니다. then 은 두 개의 콜백 함수를 인자로 전달받으며 첫번째 콜백 함수는 프로미스가 fulfilled 상태가 되면 호출되고 두 번째 콜백 함수는 프로미스가 rejected 상태가 되면 호출됩니다. 이때 첫 번째 콜백 함수는 프로미스의 비동기 처리 결과를 인수로 전달받고 두 번째 콜백 함수는 에러를 인수로 전달받습니다. catch 메서드는 한 개의 콜백 함수를 인자로 전닯다는데 프로미스가 rejected 상태인 경우만 호출되므로 에러 처리에 용이하게 쓰이며 finally 는 비동기 처리 결과에 상관없이 수행하는 후속 처리를 담당하게 됩니다. 이 때 이 세가지 후속처리 메서드 모두 프로미스를 반환한다는 공통점이 있습니다. 이때 프로미스는 기존의 콜백에 비해서 비동기 처리에 대한 상태와 결과를 저장하는 프로미스를 반환함녀 후속 처리 메서드를 사용해 인자로 콜백 함수를 전달해야 하는 불편함은 해소했지만 여전히 콜백 패턴을 따르고 있어 프로미스 체이닝을 통해 then 을 중첩적으로 사용해야 해 가독성이 나빠진다는 문제가 잔류합니다. 이를 해결하기 위해 async await 를 사용하게 됩니다.

</aside>

<aside>
3️⃣ **다음 함수를 실행 했을 때 콘솔에 출력되는 결과는?**

```jsx
var func = () => {
  for (var i = 0; i < 3; i++) {
    setTimeout(() => {
      console.log(i);
    }, 1000 * i);
  }
};
func();
```

문제 출처: https://jongbeom-dev.tistory.com/118

setTimeout 이 비동기적으로 동작하는 비동기 함수이며 func 은 비동기 함수를 포함하는 함수일 뿐이므로, func 의 호출이 종료된 이후 setTimeout 이 호출되어 3이 3번 출력될 것 같습니다. (1초 간격으로)

</aside>