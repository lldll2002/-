## 자바스크립트 프로토타입

- 프로토타입 정의

| 개념 | 설명 |
|------|------|
| 프로토타입 객체 | JavaScript에서 모든 객체는 `prototype` 객체를 가집니다. 이 객체는 다른 객체에 속성이나 메서드를 상속하는 데 사용됩니다. |
| 상속 메커니즘 | 객체가 특정 속성이나 메서드에 접근하려 할 때, 해당 속성이나 메서드가 해당 객체에 없으면 JavaScript는 객체의 프로토타입 체인을 따라 올라가면서 해당 속성이나 메서드를 찾습니다. |
| 프로토타입 체인 | 프로토타입은 계층적으로 연결될 수 있어, 한 객체의 프로토타입이 다른 객체의 프로토타입을 가리킬 수 있습니다. 이러한 연결을 프로토타입 체인이라고 합니다. |

- 프로토타입 예제

JavaScript의 배열은 Array.prototype에서 메서드와 속성을 상속받습니다. 따라서 모든 배열은 Array.prototype에 정의된 메서드(push, pop, forEach 등)를 사용할 수 있습니다.

```js
let myArray = [1, 2, 3];
myArray.push(4); // myArray는 Array.prototype의 메서드를 상속받음
```

- 프로토타입 장점과 단점

| 장점 | 설명 |
|------|------|
| 메모리 효율 | 같은 생성자로 생성된 모든 객체가 메서드를 공유하기 때문에, 각 객체가 메서드의 복사본을 가지고 있을 필요가 없어 메모리를 절약할 수 있습니다. |
| 재사용성 | 공통된 특성과 행위를 가진 객체들을 쉽게 만들 수 있어, 코드의 재사용성과 관리 용이성이 증가합니다. |

| 단점 | 설명 |
|------|------|
| 오버라이딩의 복잡성 | 하위 객체에서 상위 객체의 메서드를 오버라이드(재정의)할 때 예상치 못한 결과가 발생할 수 있습니다. |
| 속성 공유의 문제 | 프로토타입을 통해 상속받은 속성이 참조 타입일 경우, 한 객체에서 이 속성을 변경하면 다른 모든 객체에도 영향을 미칩니다. |



| 개념 | 설명 |
|------|------|
| 프로퍼티 Getter와 Setter | 객체의 특정 프로퍼티에 접근하거나 수정할 때 호출되는 특별한 메서드입니다. `get`과 `set`을 사용하여 정의되며, 데이터 검증이나 계산된 속성을 제공하는 데 유용합니다. |
| 함수의 Prototype 프로퍼티 | 모든 함수는 `prototype` 속성을 가지며, 이는 함수가 생성자로 사용될 때 생성된 객체의 프로토타입으로 설정됩니다. 이를 통해 생성자 함수의 인스턴스들이 메서드와 속성을 공유할 수 있습니다. |
| 프로토타입 메서드와 __proto__가 없는 객체 | 프로토타입 메서드는 객체가 직접 메서드를 소유하지 않고 프로토타입 체인을 통해 공유하는 메서드입니다. `__proto__`가 없는 객체는 `Object.create(null)`로 생성되며, 표준 내장 객체의 속성이나 메서드를 상속받지 않습니다. |


```js
// 프로퍼티 Getter와 Setter
let person = {
  firstName: 'John',
  lastName: 'Doe',

  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },

  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ');
  }
};

console.log(person.fullName); // "John Doe"
person.fullName = 'Jane Smith';
console.log(person.fullName); // "Jane Smith"


// 함수의 prototype 프로퍼티
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function() {
  console.log(`${this.name} makes a noise.`);
};

const dog = new Animal('Dog');
dog.speak(); // "Dog makes a noise."


// __proto__가 없는 객체
const myObject = Object.create(null); // __proto__가 없는 객체 생성

console.log(myObject.__proto__); // undefined
console.log(Object.getPrototypeOf(myObject)); // null

// 표준 내장 객체의 메서드를 상속받지 않음
// myObject.toString(); // TypeError: myObject.toString is not a function
```