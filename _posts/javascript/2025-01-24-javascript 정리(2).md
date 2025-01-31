---
published: true
title: "Java Script 이론 정리(2)"
date: 2025-01-24
toc: true
toc_sticky: true
category: 
  - javascript
tags:
  - javascript이론
---

## **18. Proxy와 Reflect**
ES6에서 도입된 `Proxy`와 `Reflect`는 객체의 동작을 가로채고 조작할 수 있는 강력한 기능을 제공한다.

### **(1) Proxy 개념**
`Proxy`는 객체에 대한 작업(속성 접근, 수정 등)을 가로채서 원하는 방식으로 제어할 수 있도록 해준다.

```javascript
const user = {
    name: "박일범",
    age: 30
};

const handler = {
    get(target, prop) {
        if (prop in target) {
            return target[prop];
        } else {
            return "존재하지 않는 속성입니다.";
        }
    },
    set(target, prop, value) {
        if (prop === "age" && value < 0) {
            console.log("나이는 0 이상이어야 합니다.");
            return false;
        }
        target[prop] = value;
        return true;
    }
};

const proxyUser = new Proxy(user, handler);

console.log(proxyUser.name);  // 박일범
console.log(proxyUser.gender);  // 존재하지 않는 속성입니다.
proxyUser.age = -5;  // 나이는 0 이상이어야 합니다.
```

### **(2) Reflect API**
`Reflect` 객체는 `Proxy`와 함께 사용되며, 객체 조작을 보다 직관적으로 할 수 있게 도와준다.

```javascript
const obj = { a: 10 };

console.log(Reflect.get(obj, "a"));  // 10
Reflect.set(obj, "b", 20);
console.log(obj.b);  // 20
```

---

## **19. 제너레이터 함수 (Generator Function)**
제너레이터 함수는 실행을 중단(`yield`)하고 다시 재개(`next()`)할 수 있는 특수한 함수이다.

### **(1) 기본적인 사용법**
```javascript
function* generatorFunc() {
    yield 1;
    yield 2;
    yield 3;
}

const gen = generatorFunc();
console.log(gen.next());  // { value: 1, done: false }
console.log(gen.next());  // { value: 2, done: false }
console.log(gen.next());  // { value: 3, done: false }
console.log(gen.next());  // { value: undefined, done: true }
```

### **(2) 반복 가능한 이터레이터 만들기**
```javascript
function* infiniteCounter() {
    let count = 0;
    while (true) {
        yield count++;
    }
}

const counter = infiniteCounter();
console.log(counter.next().value);  // 0
console.log(counter.next().value);  // 1
console.log(counter.next().value);  // 2
```

---

## **20. WeakMap과 WeakSet**
`WeakMap`과 `WeakSet`은 가비지 컬렉션(GC)에 의해 자동으로 메모리에서 관리되는 컬렉션이다.

### **(1) WeakMap**
- 키로 객체만 사용할 수 있음
- 자동으로 가비지 컬렉션됨

```javascript
let obj = { name: "박일범" };
const weakMap = new WeakMap();
weakMap.set(obj, "개발자");

console.log(weakMap.get(obj));  // 개발자
obj = null;  // obj가 메모리에서 제거됨
```

### **(2) WeakSet**
- 객체만 저장 가능
- 중복이 없음

```javascript
let user1 = { name: "철수" };
let user2 = { name: "영희" };

const weakSet = new WeakSet();
weakSet.add(user1);
weakSet.add(user2);

console.log(weakSet.has(user1));  // true
user1 = null;  // user1이 가비지 컬렉션됨
```

---

## **21. 정규 표현식 (RegExp)**
정규 표현식은 문자열에서 특정 패턴을 찾거나 치환하는 데 사용된다.

### **(1) 정규 표현식 테스트**
```javascript
const regex = /hello/i;  // 대소문자 구분 없이 "hello" 찾기
console.log(regex.test("Hello World"));  // true
```

### **(2) 문자열 검색**
```javascript
const text = "이메일 주소는 example@email.com 입니다.";
const emailPattern = /\S+@\S+\.\S+/;
const email = text.match(emailPattern);
console.log(email[0]);  // example@email.com
```

### **(3) 문자열 치환**
```javascript
const sentence = "바나나 바나나 바나나";
const newSentence = sentence.replace(/바나나/g, "사과");
console.log(newSentence);  // 사과 사과 사과
```

---

## **22. 웹 워커 (Web Workers)**
웹 워커는 백그라운드에서 실행되는 스레드로, 메인 스레드와 별개로 작업을 수행할 수 있다.

### **(1) 웹 워커 생성**
```javascript
// worker.js
self.onmessage = function(event) {
    let result = event.data * 2;
    self.postMessage(result);
};
```

### **(2) 웹 워커 사용**
```javascript
const worker = new Worker("worker.js");
worker.postMessage(10);

worker.onmessage = function(event) {
    console.log("결과:", event.data);  // 20
};
```

---

## **23. Service Worker와 PWA**
**Service Worker**는 오프라인에서도 웹을 사용할 수 있도록 도와주는 API로, PWA(Progressive Web App)의 핵심 기술이다.

### **(1) 서비스 워커 등록**
```javascript
if ("serviceWorker" in navigator) {
    navigator.serviceWorker.register("/sw.js")
        .then(() => console.log("Service Worker 등록 완료"))
        .catch(err => console.log("등록 실패", err));
}
```

### **(2) 캐싱을 활용한 오프라인 지원 (`sw.js`)**
```javascript
self.addEventListener("install", event => {
    event.waitUntil(
        caches.open("v1").then(cache => {
            return cache.addAll(["/", "/index.html", "/styles.css"]);
        })
    );
});

self.addEventListener("fetch", event => {
    event.respondWith(
        caches.match(event.request).then(response => {
            return response || fetch(event.request);
        })
    );
});
```

---

## **24. WebAssembly (WASM)**
자바스크립트보다 빠르게 실행되는 바이너리 포맷을 실행할 수 있도록 하는 기술이다.  

### **(1) WebAssembly 파일 로드**
```javascript
fetch("module.wasm")
    .then(response => response.arrayBuffer())
    .then(bytes => WebAssembly.instantiate(bytes))
    .then(result => console.log(result.instance.exports.add(2, 3)));
```

---

## **25. 최신 ECMAScript(ES2023+) 문법**
### **(1) 배열 `findLast()`, `findLastIndex()`**
```javascript
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.findLast(n => n % 2 === 0));  // 4
console.log(numbers.findLastIndex(n => n % 2 === 0));  // 3
```

### **(2) `Array.prototype.toSorted()`**
원본 배열을 변경하지 않고 정렬된 새로운 배열 반환
```javascript
const arr = [3, 1, 2];
console.log(arr.toSorted());  // [1, 2, 3]
console.log(arr);  // [3, 1, 2] (원본 유지)
```

---

## **26. Web Components (웹 컴포넌트)**
웹 컴포넌트는 HTML, CSS, JavaScript를 캡슐화하여 재사용 가능한 UI 요소를 만들 수 있도록 하는 기술이다.

### **(1) 웹 컴포넌트 생성 (Custom Elements)**
```javascript
class MyButton extends HTMLElement {
    constructor() {
        super();
        this.innerHTML = `<button>클릭하세요</button>`;
    }
}
customElements.define("my-button", MyButton);
```
🔹 HTML에서 사용 가능  
```html
<my-button></my-button>
```

### **(2) Shadow DOM 적용**
```javascript
class ShadowButton extends HTMLElement {
    constructor() {
        super();
        const shadow = this.attachShadow({ mode: "open" });
        shadow.innerHTML = `
            <style>button { background: blue; color: white; }</style>
            <button>Shadow DOM 버튼</button>
        `;
    }
}
customElements.define("shadow-button", ShadowButton);
```

---

## **27. Intl (국제화 API)**
`Intl` 객체는 날짜, 시간, 숫자 등을 다양한 언어 및 형식으로 변환하는 기능을 제공한다.

### **(1) 날짜 포맷 변환**
```javascript
const date = new Date();
const formattedDate = new Intl.DateTimeFormat("ko-KR").format(date);
console.log(formattedDate);  // 2025. 2. 1.
```

### **(2) 통화 형식 변환**
```javascript
const price = 123456.78;
const formattedPrice = new Intl.NumberFormat("ko-KR", {
    style: "currency",
    currency: "KRW"
}).format(price);
console.log(formattedPrice);  // ₩123,457
```

---

## **28. WebRTC (실시간 통신)**
WebRTC는 브라우저 간 음성, 영상, 데이터 통신을 가능하게 한다.

### **(1) 사용자 카메라 스트리밍**
```javascript
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
    .then(stream => {
        document.querySelector("video").srcObject = stream;
    })
    .catch(error => console.error("카메라 접근 실패:", error));
```

---

## **29. WebSockets (실시간 데이터 통신)**
WebSocket은 서버와 클라이언트 간 양방향 실시간 통신을 지원하는 프로토콜이다.

### **(1) WebSocket 서버 연결**
```javascript
const socket = new WebSocket("wss://example.com/socket");

socket.onopen = () => {
    console.log("서버에 연결됨");
    socket.send("안녕하세요!");
};

socket.onmessage = event => {
    console.log("서버로부터 메시지 수신:", event.data);
};

socket.onclose = () => console.log("연결 종료");
```

---

## **30. OffscreenCanvas (백그라운드 캔버스)**
OffscreenCanvas는 웹 워커에서 캔버스를 렌더링할 수 있도록 한다.

### **(1) 기본 사용법**
```javascript
const offscreen = new OffscreenCanvas(300, 300);
const ctx = offscreen.getContext("2d");

ctx.fillStyle = "red";
ctx.fillRect(0, 0, 100, 100);
```

---

## **31. Broadcast Channel API (브라우저 간 메시지 공유)**
Broadcast Channel API는 같은 도메인의 여러 탭에서 데이터를 공유할 수 있도록 한다.

### **(1) 데이터 전송**
```javascript
const channel = new BroadcastChannel("chat");
channel.postMessage("안녕하세요!");
```

### **(2) 데이터 수신**
```javascript
const channel = new BroadcastChannel("chat");
channel.onmessage = event => console.log("수신된 메시지:", event.data);
```

---

## **32. File System Access API (파일 시스템 접근)**
사용자의 파일 시스템에 직접 접근하여 읽기 및 쓰기가 가능하다.

### **(1) 파일 열기**
```javascript
async function openFile() {
    const [fileHandle] = await window.showOpenFilePicker();
    const file = await fileHandle.getFile();
    console.log(file.name);
}
```

### **(2) 파일 저장**
```javascript
async function saveFile() {
    const newHandle = await window.showSaveFilePicker();
    const writable = await newHandle.createWritable();
    await writable.write("파일 내용 저장");
    await writable.close();
}
```

---

## **33. Navigator API (브라우저 정보 확인)**
Navigator API는 사용자의 브라우저 및 장치 정보를 가져올 수 있다.

### **(1) 사용자 브라우저 정보 가져오기**
```javascript
console.log(navigator.userAgent);
console.log(navigator.language);
```

### **(2) 온라인/오프라인 상태 확인**
```javascript
window.addEventListener("online", () => console.log("온라인 상태"));
window.addEventListener("offline", () => console.log("오프라인 상태"));
```

---

## **34. Web Animations API (자바스크립트 애니메이션)**
CSS 애니메이션을 자바스크립트에서 제어할 수 있다.

### **(1) 애니메이션 적용**
```javascript
const element = document.querySelector(".box");
element.animate([
    { transform: "translateX(0px)" },
    { transform: "translateX(100px)" }
], {
    duration: 1000,
    iterations: Infinity
});
```

---

## **35. Hyper-Threading을 활용한 WebAssembly + Web Workers**
WebAssembly와 Web Workers를 결합하여 성능을 극대화할 수 있다.

```javascript
const worker = new Worker("wasm-worker.js");
worker.postMessage({ num: 10 });

worker.onmessage = event => {
    console.log("결과:", event.data);
};
```
📌 WebAssembly를 활용하면 연산 속도를 네이티브 수준으로 끌어올릴 수 있다.

---