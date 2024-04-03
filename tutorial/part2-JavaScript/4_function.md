## 자바스크립트 함수

- 함수 종류  

| 용어 | 설명 | 예시 |
| --- | --- | --- |
| [함수 선언식 (Function Declaration)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/function) | 함수를 정의하고 이름을 지정하는 방식으로, `function` 키워드를 사용하여 함수를 선언합니다. |`function bread() {}` |
| [함수 표현식 (Function Expression)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/function) | 변수에 함수를 할당하는 방식으로, 익명 함수를 만들고 변수에 할당하여 사용합니다. |`const bread = function() {}` |
| [화살표 함수 (Arrow Function)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions) | ES6에서 도입된 간결한 문법으로, `=>` 기호를 사용하여 함수를 선언합니다. | `const bread = () => {}` |
| [익명 함수 (Anonymous Function)](https://developer.mozilla.org/ko/docs/Glossary/Function) | 이름이 없는 함수로, 함수 표현식이나 콜백 함수로 주로 사용됩니다. | `setTimeout(function() { console.log('Hello') }, 1000)` |
| [즉시 실행 함수 (Immediately Invoked Function Expression, IIFE)](https://developer.mozilla.org/ko/docs/Glossary/IIFE) | 정의되자마자 즉시 실행되는 함수로, 함수를 선언하고 즉시 괄호로 둘러싸서 호출합니다. | `(function() { console.log('I am invoked immediately') })()` |

```js
// 함수 선언식 (Function Declaration)
function bread() {
  console.log("This is a bread function declaration");
}

// 함수 표현식 (Function Expression)
const breadFunc = function() {
  console.log("This is a bread function expression");
};

// 화살표 함수 (Arrow Function)
const breadArrow = () => {
  console.log("This is a bread arrow function");
};

// 익명 함수 (Anonymous Function)
setTimeout(function() {
  console.log('Hello');
}, 1000);

// 즉시 실행 함수 (Immediately Invoked Function Expression, IIFE)
(function() {
  console.log('I am invoked immediately');
})();
```

<br/><br/>

## 지역변수와 전역변수, 메서드, 매개변수(parameter) 와 전달 인자(argument)

<span style="color: orange;">자바스크립트에서 자주 등장하는 용어</span>  

| 용어 | 설명 |
|-----|-----|
| [지역변수](https://developer.mozilla.org/ko/docs/Glossary/Local_variable) | 함수 내부에서 선언된 변수로, 해당 함수 내부에서만 접근할 수 있습니다. |
| [전역변수](https://developer.mozilla.org/ko/docs/Glossary/Global_variable) | 함수 외부에서 선언된 변수로, 스크립트 전체에서 접근할 수 있습니다.   |
| [메서드](https://developer.mozilla.org/ko/docs/Glossary/Method) | 객체에 속한 함수를 의미하며, 해당 객체의 속성으로써 동작합니다. |
| [매개변수(parameter)](https://developer.mozilla.org/ko/docs/Glossary/Parameter) | 함수 안에서의 정의 및 사용에 나열되어 있는 변수들을 의미합니다. |
| [전달 인자(argument)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments) | 함수를 호출할 때 전달되는 실제 값을 의미합니다. |
| [this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this) | 현재 실행 중인 코드에서 사용되는 객체를 가리키는 키워드로, 주로 메서드 내부에서 사용됩니다.<br/>해당 메서드를 호출한 객체를 가리키거나, 함수가 어디서 호출되었는지에 따라 동적으로 결정될 수 있습니다.<br/> ES2015에서는 화살표 함수에서는 자체적인 this 바인딩을 제공하지 않습니다. |

<span style="color: orange;">지역변수 (Local Variable)</span>  

```js
function bakery() {
  const cheeseBread = "치즈빵"; // 함수 내부에서만 접근할 수 있는 지역 변수
  console.log(cheeseBread);
}

bakery(); // 출력: 치즈빵
// console.log(cheeseBread); // 오류: cheeseBread is not defined (지역 변수이므로 함수 외부에서 접근 불가)
```
<span style="color: orange;">전역변수 (Global Variable)</span>  

```js
const saltBread = "소금빵";

function cafe() {
  console.log(saltBread); // 함수 내부에서 전역 변수에 접근 가능
}

cafe(); // 출력: 소금빵
console.log(saltBread); // 출력: 소금빵 (전역 변수라서 함수 외부에서도 접근 가능)
```

<span style="color: orange;">매개변수(parameter)와 전달 인자(argument)</span>  

```js
function shop(bread) {
  // 함수 내에서 사용되는 변수 'bread'는 매개변수(parameter)입니다.
  console.log("맛있는 " + bread + "!");
}

const saltBread = "소금빵";
const chocoBread = "초코빵";
// shop(saltBread)에서 saltBread가 인자입니다.
shop(saltBread); // 맛있는 소금빵!
```

<span style="color: orange;">메서드 (Method), this</span>  

```js
const order = {
  drink: "아메리카노",
  size: "Tall",
  makeDrink: function() {
    // makeDrink 메서드 내부에서 this.drink와 this.size를 사용하면 현재 order 객체의 속성에 접근할 수 있습니다. this는 메서드가 호출될 때 호출된 객체에 바인딩되므로, makeDrink 메서드가 order 객체에서 호출될 때 this는 order 객체를 가리키게 됩니다.
    // 객체 내에 함수로 정의된 속성은 키(key)로도 부를 수 있고, 메서드로도 부를 수 있습니다. 
    console.log("사이즈 : " + this.drink + ", 종류 : " + this.size);
  }
};

order.makeDrink(); // 사이즈 : 아메리카노, 종류 : Tall
```


<br/><br/>

## 생성자 함수 

- 일반 함수와 생성자 함수 차이

| 목적 | 생성자 함수 | 일반 함수 |
|------|-------------|------------|
|   | 객체를 생성하는 데 주로 사용됩니다. 일반적으로 `new` 키워드와 함께 호출됩니다. | 다양한 작업을 수행하거나 값을 반환하는 데 사용됩니다. |
| 호출 방식 | `new` 키워드를 사용하여 객체 인스턴스를 생성합니다. | 호출하는 동안 `new` 키워드를 사용하지 않습니다. |
| 반환 값 | 일반적으로 명시적인 반환문이 없는 경우에도 객체를 반환합니다. | 명시적으로 반환된 값이 있거나 아무 값도 반환하지 않을 수 있습니다. |
| 이름 관례 | 일반적으로 첫 글자를 대문자로 시작하여 이름을 짓습니다. 예: `function Person() {}` | 소문자 또는 대문자로 이름을 짓습니다. |
| 사용 패턴 | 동일한 구조의 여러 객체를 생성할 때 사용됩니다. | 특정 작업을 수행하기 위해 호출됩니다. |


<span style="color: orange;">new Function()</span>  

```js
// new Function을 사용하여 함수 생성
let sum = new Function('a', 'b', 'return a + b');

console.log(sum(2, 3)); // 5

// 여러 매개변수와 복잡한 로직을 포함하는 함수
let complexFunction = new Function('a', 'b', 'if(a > b) { return a * b; } else { return a + b; }');

console.log(complexFunction(3, 2)); // 6 (3 * 2)
console.log(complexFunction(2, 3)); // 5 (2 + 3)
```

<span style="color: orange;">this, 메서드(call, apply, bind), 함수표현식(arrow function)</span>  

| 메서드 | 설명 |
|--------|------|
| [Function.prototype.call()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/call) | 함수를 호출하는 메서드로, 특정 객체를 지정하여 해당 함수 내에서의 `this`를 지정된 객체로 설정합니다. 이때, 함수의 매개변수는 순차적으로 전달됩니다. |
| [Function.prototype.apply()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) | 함수를 호출하는 메서드로, 특정 객체를 지정하여 해당 함수 내에서의 `this`를 지정된 객체로 설정합니다. `call()`과 유사하지만, 함수의 매개변수를 배열로 전달합니다. |
| [Function.prototype.bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) | 함수를 호출하는 메서드로, 특정 객체를 지정하여 해당 함수 내에서의 `this`를 지정된 객체로 설정한 새로운 함수를 생성합니다. 이때, 기존 함수와 동일한 매개변수를 전달하여 새로운 함수를 호출할 수 있습니다. |


```js
// 빵 가게 정의
const bakery = {
  breadType: "바게트",
  flavor: "허니버터",
};

// 빵 굽기 함수
function bakeBread() {
  console.log("🥖 " + this.breadType + " 빵이 구워졌습니다. 맛은 " + this.flavor + "입니다.");
}

// 빵 굽기 - call 방식
bakeBread.call(bakery); // 출력: 🥖 바게트 빵이 구워졌습니다. 맛은 허니버터입니다.

// 빵 굽기 - apply 방식
bakeBread.apply(bakery); // 출력: 🥖 바게트 빵이 구워졌습니다. 맛은 허니버터입니다.

// 빵 굽기 - bind 방식
const boundBreadFunction = bakeBread.bind(bakery);
boundBreadFunction(); // 출력: 🥖 바게트 빵이 구워졌습니다. 맛은 허니버터입니다.

// 화살표 함수로 빵 굽기
const bakeBreadArrow = () => {
  console.log("🥖 " + this.breadType + " 빵이 구워졌습니다. 맛은 " + this.flavor + "입니다.");
};

bakeBreadArrow.call(bakery); // 출력: 🥖 undefined 빵이 구워졌습니다. 맛은 undefined입니다.
bakeBreadArrow.apply(bakery); // 출력: 🥖 undefined 빵이 구워졌습니다. 맛은 undefined입니다.
const boundBreadFunctionArrow = bakeBreadArrow.bind(bakery);
boundBreadFunctionArrow(); // 출력: 🥖 undefined 빵이 구워졌습니다. 맛은 undefined입니다.
```

## 재귀함수

| 재귀(Recursion) |
|------------------|
| 재귀는 함수가 자기 자신을 호출하는 것을 의미합니다. |
| 재귀는 보통 함수 내에서 어떤 작업을 반복하면서 처리할 때 사용됩니다. |
| 재귀 함수는 종료 조건을 반드시 가져야 합니다. 종료 조건이 없으면 함수가 무한히 호출되어 스택 오버플로우와 같은 문제가 발생할 수 있습니다. |


팩토리얼은 양의 정수 n에 대해 n부터 1까지의 모든 정수를 곱한 값을 의미합니다. 일반적으로 n!으로 표기하며, 수학적으로는 다음과 같이 정의됩니다.

`n! = n × (n - 1) × (n - 2) × ... × 2 × 1`

예를 들어, 5!는 다음과 같이 계산됩니다.

`5! = 5 × 4 × 3 × 2 × 1 = 120`

팩토리얼은 조합론 및 확률론에서 자주 사용되며, 알고리즘 및 프로그래밍 연습에서도 자주 등장합니다.

```js
function factorial(n) {
  // 종료 조건: n이 1 이하일 때 1을 반환
  if (n <= 1) {
    return 1;
  }
  // 재귀 호출: n에 대한 팩토리얼을 구하고 n을 곱함
  return n * factorial(n - 1);
}

// 팩토리얼 계산 예제
console.log(factorial(5)); // 출력: 120

function factorial(n) {
  // 종료 조건: n이 1 이하일 때, 1을 반환
  if (n <= 1) {
    return 1;
  }
  // 재귀 호출: n에 대한 팩토리얼을 구하고 n을 곱함
  return n * factorial(n - 1);
}

// 팩토리얼 계산 예제
console.log(factorial(3)); // 출력: 6

```

## Class

- JavaScript에서 클래스(class)는 객체 생성을 위한 템플릿으로 사용됩니다.
- 객체 지향 프로그래밍의 중요한 구성 요소인 클래스는 데이터(속성)와 이를 조작하는 메서드를 하나의 단위로 묶어 관리합니다.
- 클래스는 특정 데이터 구조와 관련된 기능을 함께 캡슐화하고 구조화하는 중요한 역할을 수행합니다.
- 자바스크립트에서, 클래스는 기술적으로 함수의 한 종류로 간주됩니다.

| 개념 | 설명 |
|------|------|
| 생성자(Constructor) | 클래스를 통해 객체가 생성될 때 자동으로 호출되는 특별한 메서드입니다. 일반적으로 객체의 초기 상태를 설정하는 데 사용됩니다. |
| 속성(Properties) | 클래스에 의해 생성된 객체들이 가질 수 있는 변수나 데이터입니다. |
| 메서드(Methods) | 클래스 내에서 정의된 함수로, 클래스가 가지고 있는 데이터를 조작하거나 계산하는 데 사용됩니다. |
| 상속(Inheritance) | 한 클래스가 다른 클래스의 특성을 상속받아 사용할 수 있습니다. 이를 통해 코드의 재사용성과 유지보수성이 향상됩니다. |
| 캡슐화(Encapsulation) | 데이터(속성)와 그 데이터를 조작하는 메서드를 하나로 묶음으로써 정보 은닉을 가능하게 합니다. |

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello, my name is ${this.name}`;
  }
}

const person = new Person("Alice");
console.log(typeof Person);  // "function"
console.log(person.greet()); // "Hello, my name is Alice"
```

- 클래스 선언과 표현식

| 구분 | 방법 | 설명 |
|------|------|------|
| 클래스 선언 | `class MyClass {}` | 클래스 선언은 `class` 키워드 다음에 클래스 이름을 명시하고, 중괄호(`{}`) 안에 클래스의 속성과 메서드를 정의하는 방식입니다. |
| 클래스 표현식 | `const MyClass = class {}` | 클래스 표현식은 클래스를 변수에 할당하는 방식입니다. 클래스에 이름을 주거나 이름을 생략할 수 있으며, 이는 함수 표현식과 유사합니다. |

클래스 정의는 클래스 선언(class MyClass {}) 또는 클래스 표현식(const MyClass = class {})을 통해 이루어지며, 이는 함수를 정의하는 방법과 유사합니다. 자바스크립트의 클래스는 객체 지향적인 프로그래밍 접근을 가능하게 하는 함수 기반의 구조로 볼 수 있습니다.

- 클래스와 함수의 관계

| 주제 | 설명 |
|------|------|
| 클래스는 함수의 확장 | 자바스크립트에서 클래스는 사실상 '특별한 형태의 함수'입니다. 클래스 선언(`class MyClass {}`) 또는 클래스 표현식(`const MyClass = class {}`)을 통해 정의되며, 내부적으로는 함수로 처리됩니다. |
| 생성자 함수 | 전통적인 자바스크립트에서 객체 생성을 위해 사용되는 생성자 함수(constructor function)와 클래스는 유사한 역할을 합니다. 하지만 클래스 문법은 생성자 함수보다 훨씬 명확하고 직관적인 객체 지향 프로그래밍을 가능하게 합니다. |
| 함수로서의 속성 | 클래스를 콘솔에 출력하면 함수로 표시됩니다. 이는 자바스크립트 엔진이 클래스를 함수로 처리하기 때문입니다. |
| 메서드 정의 | 클래스 내부에서 메서드를 정의할 때는 함수 문법을 사용합니다. |

- constructor

| 구분 | 설명 |
|------|------|
| 선택 사항 | 클래스에서 `constructor`를 생략할 수 있습니다. 이 경우, 자바스크립트 엔진이 기본 `constructor`를 자동으로 제공합니다. |
| 자동 생성 | `constructor`가 명시적으로 정의되지 않은 경우, 클래스는 빈 `constructor`를 가지고 있는 것으로 간주됩니다. 즉, 인스턴스를 생성할 때 아무런 작업도 수행하지 않는 기본 생성자가 존재하는 것과 동일합니다. |
| 초기화 작업 | `constructor`를 사용하는 주된 이유는 새로 생성된 객체의 초기 상태를 설정하는 것입니다. 속성 값을 설정하거나 필요한 초기화 작업을 수행합니다. |
| 상속에서의 역할 | 상속받은 클래스에서 `constructor`를 정의할 때는 `super` 키워드를 사용하여 부모 클래스의 `constructor`를 호출해야 합니다. 이것은 부모 클래스의 생성 로직을 실행시키기 위해 필요합니다. |

constructor 메서드는 클래스에서 객체를 생성하고 초기화하는데 사용되지만, 모든 클래스에 반드시 있어야 하는 것은 아닙니다. 예를 들어, constructor가 없는 간단한 클래스는 다음과 같이 정의할 수 있습니다.

```js
class MyClass {
  myMethod() {
    console.log('Hello, World!');
  }
}

const myInstance = new MyClass();
myInstance.myMethod(); // "Hello, World!" 출력
```

- Private과 Protected 프로퍼티와 메서드

| 유형 | 설명 |
|------|------|
| private 프로퍼티/메서드 | 클래스 내부에서만 접근 및 사용이 가능한 프로퍼티나 메서드입니다. JavaScript에서는 private 필드를 `#` 기호를 사용하여 선언합니다. 이는 클래스 외부에서 접근할 수 없어 데이터 캡슐화와 보안성을 향상시킵니다. |
| protected 프로퍼티/메서드 | 클래스 자체와 그 자식 클래스에서만 접근할 수 있는 프로퍼티나 메서드입니다. JavaScript에서는 공식적인 `protected` 지원이 없지만, 관례적으로 `_` (언더스코어) 접두사를 사용하여 표시하는 경우가 많습니다. |


```js
class MyClass {
  #privateField;   // private 프로퍼티 선언. 클래스 내부에서만 접근 가능합니다.
  _protectedField; // protected 프로퍼티 선언. 클래스 내부와 상속받은 자식 클래스에서 접근 가능합니다.

  constructor() {
    this.#privateField = "private";     // private 프로퍼티 초기화
    this._protectedField = "protected"; // protected 프로퍼티 초기화
  }

  #privateMethod() {
    console.log('이것은 private 메서드입니다.'); // private 메서드 정의. 클래스 내부에서만 호출 가능합니다.
  }

  _protectedMethod() {
    console.log('이것은 protected 메서드입니다.'); // protected 메서드 정의. 클래스 내부와 상속받은 자식 클래스에서 호출 가능합니다.
  }
}

const myInstance = new MyClass(); // MyClass의 인스턴스 생성
// myInstance.#privateField;  // SyntaxError. Private 필드에 외부에서 접근 시도, 접근할 수 없습니다.
// myInstance.#privateMethod();  // SyntaxError. Private 메서드에 외부에서 호출 시도, 호출할 수 없습니다.
console.log(myInstance._protectedField); // protected 필드 접근 가능. 출력: "protected"
myInstance._protectedMethod(); // protected 메서드 호출 가능. 출력: "이것은 protected 메서드입니다."
```