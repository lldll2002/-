## 자바스크립트 반복문 (while, for, switch)

반복문 (loop)

- [while](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/while) : 조건문이 참일 때 실행되는 반복문
    
```jsx
// 초기 값
let n = 0;
let x = 0;

// true 일때만 실행
while (n < 3) {
  n++;    // ++는  n = n + 1
  x += n; // x +=는  x = x + n
  console.log('n' + n);
  console.log('x' + x);
}

console.log(n) // 3
/*
0 < 3 true
1 < 3 true
2 < 3 true
3 < 3 while 의 조건이 false 가 되었기 때문에 탈출
*/

console.log(x) // 6
/*
n++ = n + 1  ->     1,     2,     3
x = x + n    ->

첫번째 루프
0(초기 값)+1(n은 1) = 1 (할당)

두번째 루프 돌았을 때, n 이 1이었는데 n이 1개가 더해져서 2가 됨
1(할당된 값)+2(n은 2) = 3 (할당)

세번째 루프 돌았을 때, n 이 2였는데 n이 1개가 더해져서 3이 됨
3(할당된 값)+3(n은 3) = 6 (할당)
*/
```

- [for](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for) : 괄호로 감싸고 세미콜론으로 구분한 세 개의 선택식과, 반복을 수행할 문으로 이루어짐

```jsx
let str = '';

for (let i = 0; i < 9; i++) {
  str = str + i;
}

console.log(str); // 012345678
```

- [break](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/break) : 현재 반복문, `[switch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)` 문, 또는 `[label](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/label)` 문을 종료하고, 그 다음 문으로 프로그램 제어를 넘김

for문에서 구성요소 생략 표현 : `for (;;) {}`

```jsx
var i = 0;

for (;;) {
  if (i > 3) break;
  console.log(i);
  i++;
}
```

- [continue](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/continue) : 재 또는 레이블이 지정된 루프의 현재 반복에서 명령문의 실행을 종료하고 반복문의 처음으로 돌아가여 루프문의 다음 코드를 실행

```jsx
for (let i = 0; i < 10; i++) {
  console.log('첫번째 루프 : ', i); // 0~9 사이 숫자가 출력됨

  // 조건이 참이라면 남아있는 본문은 실행되지 않음
  if (i % 2 == 0) continue;

  console.log('두번째 루프 : ', i); // 1, 3, 5, 7, 9가 차례대로 출력됨
}
```

- [switch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch) : 표현식을 평가하여 일치하는 케이스를 찾고, break 문을 만날 때까지 실행하며, 일치하는 케이스가 없으면 default를 실행

```jsx
let fruit = 'apple';

switch (fruit) {
  case 'apple':
    console.log('Apple selected');
    break;
  case 'banana':
    console.log('Banana selected');
    break;
  case 'orange':
    console.log('Orange selected');
    break;
  default:
    console.log('Fruit not found');
}
```

switch 문을 if 문으로 변환

```jsx
let fruit = 'apple';

if (fruit === 'apple') {
    console.log('Apple selected');
} else if (fruit === 'banana') {
    console.log('Banana selected');
} else if (fruit === 'orange') {
    console.log('Orange selected');
} else {
    console.log('Fruit not found');
}

```

- for of & for in

[for of](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of) : [반복가능한 객체](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Iteration_protocols#iterable) (`[Array](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array)`, `[Map](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Map)`, `[Set` (en-US)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set), `[String](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)`, `[TypedArray](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/TypedArray)`, [arguments](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments) 객체 등을 포함)에 대해서 반복하고 각 개별 속성값에 대해 실행되는 문이 있는 사용자 정의 반복 후크를 호출하는 루프를 생성
[for in](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in) :  상속된 열거 가능한 속성들을 포함하여 객체에서 문자열로 키가 지정된 모든 열거 가능한 속성에 대해 반복

배열로 구성된 객체를 for of 와 for in 으로 출력

```jsx
// 1. 배열로 구성
const bread = ['소금빵', '초코빵', '소보로빵'];

// for of 로 배열 요소 출력
for (const element of bread) {
  console.log('bread 빵 종류(for of) :', element);
}

// for in 로 배열 요소 출력 (배열도 객체이므로 가능)
for (const element in bread) {
  console.log('bread 빵 종류(for in) :', bread[element]);
}
```

객체로 구성된 키와 밸류를 for of 와 for in 으로 출력

```jsx
// 2. 객체로 구성
const breads = { saltBread: '소금빵', chocoBread: '초코빵', soboroBread: '소보로빵' };

// for of 로 객체 밸류 출력
for (const value of Object.values(breads)) {
  console.log('breads 빵 종류(for of)', value);
}
// for in 으로 객체 프로퍼티 출력
for (const property in breads) {
  console.log(`breads 빵 이름(for in) : ${breads[property]}`);
}
```




1. 프로그래밍 언어
  
  저수준 프로그래밍 언어 (low-level programming language) : 일반적으로 [기계어](https://ko.wikipedia.org/wiki/%EA%B8%B0%EA%B3%84%EC%96%B4)와 [어셈블리어](https://ko.wikipedia.org/wiki/%EC%96%B4%EC%85%88%EB%B8%94%EB%A6%AC%EC%96%B4), 실행속도가 매우 빠르지만 러닝커브가 높고 유지보수가 힘든 것이 단점
  
  고수준 프로그래밍 언어 (High-level programming language) : 사람이 쉽게 이해할 수 있도록 설계, 가독성이 높고 다루기 간단하다는 장점,  [컴파일러](https://ko.wikipedia.org/wiki/%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC)나 [인터프리터](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%ED%94%84%EB%A6%AC%ED%84%B0)에 의해 [저수준 프로그래밍 언어](https://ko.wikipedia.org/wiki/%EC%A0%80%EA%B8%89_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4)로 번역되어 실행
  
2. 메모리 생존주기
  
  메모리 생존주기는 대부분의 프로그래밍 언어에서 사용함
  
  1. 필요할 때 할당합니다.                                     ← 고수준 언어는 암묵적으로 할당됨
  2. 할당된 메모리를 사용합니다. (읽기, 쓰기)         ← 모든 언어에서 명시적으로 사용됨
  3. 더 이상 필요하지 않으면 해제합니다.                ← 고수준 언어는 암묵적으로 해제됨

1. 자바스크립트 메모리
  
  [자바스크립트 메모리 관리](https://developer.mozilla.org/ko/docs/Web/JavaScript/Memory_management) 는 가비지 컬렉션에 의해 관리됨
  
  가비지 컬렉션 : JavaScript는 객체가 생성되었을 때 자동으로 메모리를 할당하고 더 이상 필요하지 않을 때 자동으로 해제함
  
  ```jsx
  // 정수와 문자열을 담기 위한 메모리 할당
  const count = 123;
  const coffee = "커피";
  
  // 오브젝트와 그 오브젝트에 포함된 값들을 담기 위한 메모리 할당
  const cafe = { starbucks: 1, ediya: null, };
  
  // 배열과 배열에 담긴 값들을 위한 메모리 할당
  const tea = [1, null, "밀크티"];
  
  // 함수를 위한 할당(함수는 호출 가능한 오브젝트)
  function bread(a) {
    return a + 2;
  }
  
  // 함수식 또한 오브젝트를 담기 위한 메모리를 할당
  someElement.addEventListener(
    "click",
    () => { someElement.style.backgroundColor = "blue"; },
    false,
  );
  
  // Date 개체를 위해 메모리를 할당
  const studyDay = new Date();
  
  // DOM 엘리먼트를 위해 메모리를 할당
  const selectDiv = document.createElement("div");
  ```