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
