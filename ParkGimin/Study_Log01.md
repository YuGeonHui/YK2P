
# Thread Async

### 비 동기적(Asynchronous)

일반적으로, 프로그램의 코드는 순차적으로 진행

다른 코어 프로세서에 다른 작업들을 움직이게 하고 작업이 완료되면 알려줄 수 있을 때, 무언가를 기다리는 것은 의미가 없다. 그 동안 다른 작업을 수행할 수 있음

⇒ 비동기 프로그래밍

- 특정 코드를 실행하느라 브라우저에게 제어권을 돌려주지 않으면 브라우저는 정지된 것 처럼
    
    동작해 보인다. ⇒ Blocking
    

### Blocking

사용자의 입력을 처리하느라 웹 앱이 프로세서에 대한 제어권을 브라우저에게 반환하지 않는 현상

Blocking code 예시

```java
const btn = document.querySelector('button');
btn.addEventListener('click', () => {
  let myDate;
  for(let i = 0; i < 10000000; i++) {
    let date = new Date();
    myDate = date
  }

  console.log(myDate);

  let pElem = document.createElement('p');
  pElem.textContent = 'This is a newly-added paragraph.';
  document.body.appendChild(pElem);
});
```

⇒ 자바스크립트의 문제점 `Single Threaded` 

### Threads

Thread는 기본적으로 프로그램이 작업을 완료하는데 사용할 수 있는 단일 프로세스

각 Thread는 한 번에 하나의 작업만 수행할 수 있음 (순차적으로 실행)

`Task A --> Task B --> Task C`

- 해결책

여러 개의 CPU 코어를 가지고 한 번에 여러 가지 일을 수행 ( `Multiple Thread` )

⇒ Multiple thread를 지원하는 프로그래밍 언어는 멀티 코어 컴퓨터의 CPU를 사용하여 

여러 작업을 동시에 처리 가능

### Single Theaded

자바스크립트는 컴퓨터가 여러 개의 CPU를 가지고 있어도 `main thread` 라 불리는 

단일 thead에서만 작업을 실행 할 수 있음

- 해결책

Web workers : 여러 개의 javaScript 청크를 동시에 실행할 수 있도록 worker라고 불리는 별도의

Thread로 보낼 수 있음

⇒ 시간이 오래 걸리는 처리는 worker를 사용해 처리하면 blocking 발생을 막을 수 있다.

```
Main thread: Task A --> Task C
Worker thread: Expensive task B
```

`BUT` 한계점

1. DOM에 접근할 수 없음 ⇒ UI를 업데이트하도록 worker에게 어떠한 지시도 직접할 수 없음
2. worker에서 실행되는 코드는 차단되지 않지만 동기적으로 실행

### Asynchronous code

Task A : 서버로부터 이미지를 가져옴

Task B : 가져온 이미지에 필터를 적용

```
Main thread: Task A --> Task B
```

적용 에러 발생!!

Task D : Task B와 Task C의 결과를 모두 사용

```
Main thread: Task A --> Task B --> |Task D|
Worker thread: Task C -----------> |      |
```

Task B와 Task C의 결과 전송 속도가 다를 시 에러 발생!!

위 문제를 해결하기 위해 브라우저를 통해 특정 작업을 비 동기적으로 실행하기 위해

Promises를 사용

```
Main thread: Task A                   Task B
    Promise:      |__async operation__|
```

Task A 작업 동안 Task B는 기다릴 수 있음 and 위의 작업은 다른 곳에서 처리가 되므로, 

`비동기 작업이 진행되는 동안 main thread가 차단되지 않는다!`
