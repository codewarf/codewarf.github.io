본문은 앞으로 공부하고 정리해보며 기억하기 위해 정리해 본 글입니다.

자바스크립트는 웹 개발에서 가장 널리 사용되는 프로그래밍 언어 중 하나이다. 클라이언트 측 동적 웹 페이지를 만들기 위해 주로 사용되지만, 최근에는 서버 사이드(Node.js)에서도 활발히 사용되고있다.  

---

## **1. 자바스크립트의 특징**  
✅ **인터프리터 언어**: 코드를 한 줄씩 해석하여 실행  
✅ **동적 타입(dynamic typing)**: 변수의 타입을 명시하지 않고 할당된 값에 따라 결정  
✅ **이벤트 기반(event-driven)**: 사용자 동작(클릭, 입력 등)에 반응하는 방식  
✅ **비동기 처리(Asynchronous)**: `setTimeout()`, `Promise`, `async/await` 등을 활용한 논블로킹 방식  
✅ **객체 기반(object-oriented)**: 프로토타입(prototype) 기반 객체지향 프로그래밍 지원  

---

## **2. 변수와 자료형**  
### **(1) 변수 선언 방식**
```javascript
var name = "박일범"; // 함수 범위, 재선언 가능 (사용 지양)
let age = 25; // 블록 범위, 재선언 불가능
const PI = 3.14; // 블록 범위, 값 변경 불가능
```
### **(2) 기본 자료형 (Primitive Type)**  
- `String`: 문자열 (`"Hello"`, `'World'`)  
- `Number`: 숫자 (`1`, `3.14`)  
- `Boolean`: 참/거짓 (`true`, `false`)  
- `Undefined`: 값이 할당되지 않음  
- `Null`: 의도적으로 값이 없음  
- `Symbol`: 고유한 값 생성  

### **(3) 참조 자료형 (Reference Type)**
- `Object`: 객체 `{ key: value }`  
- `Array`: 배열 `[1, 2, 3]`  
- `Function`: 함수  

---

## **3. 연산자**
### **(1) 산술 연산자**
```javascript
console.log(10 + 5);  // 15
console.log(10 - 5);  // 5
console.log(10 * 5);  // 50
console.log(10 / 5);  // 2
console.log(10 % 3);  // 1 (나머지 연산)
```
### **(2) 비교 연산자**
```javascript
console.log(5 == "5");   // true (값만 비교)
console.log(5 === "5");  // false (값과 타입 비교)
console.log(10 > 5);     // true
console.log(10 !== 5);   // true
```
### **(3) 논리 연산자**
```javascript
console.log(true && false);  // false (AND 연산)
console.log(true || false);  // true  (OR 연산)
console.log(!true);          // false (NOT 연산)
```

---

## **4. 제어문**
### **(1) 조건문**
```javascript
let num = 10;
if (num > 0) {
    console.log("양수입니다.");
} else if (num < 0) {
    console.log("음수입니다.");
} else {
    console.log("0입니다.");
}
```
### **(2) 반복문**
```javascript
// for 문
for (let i = 0; i < 5; i++) {
    console.log(i); 
}

// while 문
let count = 0;
while (count < 3) {
    console.log(count);
    count++;
}
```

---

## **5. 함수**
### **(1) 기본 함수 선언**
```javascript
function add(a, b) {
    return a + b;
}
console.log(add(3, 5)); // 8
```
### **(2) 화살표 함수 (Arrow Function)**
```javascript
const add = (a, b) => a + b;
console.log(add(3, 5)); // 8
```
### **(3) 즉시 실행 함수 (IIFE)**
```javascript
(function() {
    console.log("즉시 실행");
})();
```

---

## **6. 객체와 배열**
### **(1) 객체**
```javascript
let person = {
    name: "박일범",
    age: 30,
    greet: function() {
        console.log("안녕하세요, 저는 " + this.name + "입니다.");
    }
};
console.log(person.name); // 박일범
person.greet(); // 안녕하세요, 저는 박일범입니다.
```
### **(2) 배열**
```javascript
let fruits = ["사과", "바나나", "포도"];
console.log(fruits[0]); // 사과
fruits.push("오렌지"); // 배열에 추가
console.log(fruits.length); // 4
```

---

## **7. 비동기 처리**
### **(1) `setTimeout()`과 `setInterval()`**
```javascript
setTimeout(() => console.log("3초 후 실행"), 3000);
setInterval(() => console.log("1초마다 실행"), 1000);
```
### **(2) Promise**
```javascript
let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료"), 2000);
});
promise.then(result => console.log(result)); // 2초 후 "완료" 출력
```
### **(3) async/await**
```javascript
async function fetchData() {
    let response = await fetch("https://api.example.com/data");
    let data = await response.json();
    console.log(data);
}
```

---

## **8. DOM 조작**
```javascript
document.getElementById("title").innerText = "변경된 제목";
document.querySelector(".content").style.color = "blue";
document.querySelector("button").addEventListener("click", function() {
    alert("버튼 클릭됨!");
});
```

---

## **9. ES6+ 주요 문법**
✅ `let`, `const` 키워드  
✅ 템플릿 리터럴 (`${}`)  
✅ 화살표 함수 (`=>`)  
✅ 객체 분해 할당 (`const {name} = obj;`)  
✅ 스프레드 연산자 (`...arr`)  
✅ 모듈화 (`export/import`)

---

## **10. 클래스와 객체 지향 프로그래밍 (OOP)**  
자바스크립트는 프로토타입 기반 객체지향 언어지만, ES6부터 `class` 문법이 도입되어 더욱 직관적으로 객체를 생성할 수 있다.  

### **(1) 클래스 선언 및 인스턴스 생성**
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`안녕하세요, 저는 ${this.name}입니다.`);
    }
}

const person1 = new Person("박일범범", 30);
person1.greet(); // 안녕하세요, 저는 박일범입니다.
```

### **(2) 상속 (Inheritance)**
```javascript
class Student extends Person {
    constructor(name, age, grade) {
        super(name, age); // 부모 클래스의 생성자 호출
        this.grade = grade;
    }

    study() {
        console.log(`${this.name} 학생이 공부 중입니다.`);
    }
}

const student1 = new Student("김철수", 20, "A");
student1.greet();  // 부모 클래스의 메서드 사용 가능
student1.study();
```

---

## **11. 모듈 시스템 (Modules)**  
큰 프로젝트에서는 코드를 여러 파일로 나누어 관리하는 것이 좋다.  
ES6부터 `export`와 `import`를 사용한 모듈화가 가능해졌다.

### **(1) 모듈 내보내기 (`export`)**
```javascript
// utils.js
export function add(a, b) {
    return a + b;
}

export const PI = 3.14;
```

### **(2) 모듈 가져오기 (`import`)**
```javascript
// main.js
import { add, PI } from './utils.js';

console.log(add(2, 3));  // 5
console.log(PI);  // 3.14
```

### **(3) 기본 내보내기 (`export default`)**
```javascript
// math.js
export default function multiply(a, b) {
    return a * b;
}
```
```javascript
// main.js
import multiply from './math.js';

console.log(multiply(3, 4)); // 12
```

---

## **12. 에러 처리 (Error Handling)**
에러가 발생하면 프로그램이 멈출 수 있기 때문에 예외 처리가 중요하다.  

### **(1) `try...catch` 문**
```javascript
try {
    let result = 10 / 0;  // 0으로 나누기
    console.log(result);
} catch (error) {
    console.error("에러 발생:", error.message);
}
```

### **(2) `throw` 문으로 사용자 정의 에러 만들기**
```javascript
function divide(a, b) {
    if (b === 0) {
        throw new Error("0으로 나눌 수 없습니다.");
    }
    return a / b;
}

try {
    console.log(divide(10, 0));
} catch (error) {
    console.error(error.message);
}
```

---

## **13. JSON과 데이터 통신**  
웹 개발에서는 서버와 데이터를 주고받을 때 JSON(JavaScript Object Notation)을 많이 사용한다.

### **(1) 객체를 JSON 문자열로 변환 (`JSON.stringify()`)**
```javascript
const user = { name: "박일범", age: 30 };
const jsonString = JSON.stringify(user);

console.log(jsonString); // '{"name":"박일범","age":30}'
```

### **(2) JSON 문자열을 객체로 변환 (`JSON.parse()`)**
```javascript
const parsedData = JSON.parse(jsonString);
console.log(parsedData.name); // 박일범
```

---

## **14. 로컬 스토리지 (Local Storage)**
브라우저에 데이터를 저장하는 방법 중 하나이다.  

### **(1) 데이터 저장 (`localStorage.setItem()`)**
```javascript
localStorage.setItem("username", "박일범");
```

### **(2) 데이터 가져오기 (`localStorage.getItem()`)**
```javascript
const name = localStorage.getItem("username");
console.log(name); // 박일범
```

### **(3) 데이터 삭제**
```javascript
localStorage.removeItem("username"); // 특정 데이터 삭제
localStorage.clear(); // 전체 삭제
```

---

## **15. 이벤트 루프와 비동기 처리**
자바스크립트는 싱글 스레드로 동작하지만, 비동기 처리를 효율적으로 수행할 수 있다.  

### **(1) 이벤트 루프 (Event Loop)**
이벤트 루프는 자바스크립트가 비동기 작업을 어떻게 처리하는지 설명하는 개념이다.  
브라우저는 **콜 스택(Call Stack)**과 **태스크 큐(Task Queue)**를 활용해 비동기 코드를 실행한다.

```javascript
console.log("시작");

setTimeout(() => {
    console.log("2초 후 실행");
}, 2000);

console.log("끝");
```
**실행 순서:**  
1. `console.log("시작")` 실행  
2. `setTimeout()` 실행 (비동기 → 웹 API에서 처리 후 태스크 큐로 이동)  
3. `console.log("끝")` 실행  
4. 2초 후, 태스크 큐에 있던 `console.log("2초 후 실행")`이 실행  

---

## **16. 자바스크립트 디자인 패턴**
자바스크립트에서 자주 사용하는 패턴들이 있다.

### **(1) 싱글톤 패턴 (Singleton Pattern)**
객체를 하나만 생성하도록 제한하는 패턴이다.  
```javascript
const Singleton = (function() {
    let instance;
    function createInstance() {
        return { name: "Singleton Instance" };
    }
    return {
        getInstance: function() {
            if (!instance) {
                instance = createInstance();
            }
            return instance;
        }
    };
})();

const a = Singleton.getInstance();
const b = Singleton.getInstance();

console.log(a === b); // true (같은 인스턴스)
```

### **(2) 모듈 패턴 (Module Pattern)**
클로저를 활용하여 데이터를 은닉하는 패턴이다.  
```javascript
const Counter = (function() {
    let count = 0;
    
    return {
        increment: function() {
            count++;
            console.log(count);
        },
        decrement: function() {
            count--;
            console.log(count);
        }
    };
})();

Counter.increment(); // 1
Counter.increment(); // 2
Counter.decrement(); // 1
```

---

## **17. 최신 자바스크립트(ES2020+) 문법**
### **(1) 옵셔널 체이닝 (`?.`)**
객체의 속성이 존재하지 않을 때 에러 없이 `undefined`를 반환한다.
```javascript
const user = { name: "홍길동", address: { city: "서울" } };
console.log(user.address?.city);  // "서울"
console.log(user.company?.name);  // undefined
```

### **(2) 널 병합 연산자 (`??`)**
`null` 또는 `undefined`일 때 기본값을 지정할 수 있다.
```javascript
const name = null;
console.log(name ?? "기본값");  // "기본값"
```

### **(3) BigInt**
매우 큰 정수를 다룰 수 있다.
```javascript
const bigNumber = 9007199254740991n;
console.log(bigNumber + 1n);  // 9007199254740992n
```

---