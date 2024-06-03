# 객체 지향 프로그래밍이란?

객체 지향 프로그래밍(OOP)은 프로그램을 객체라는 단위로 구성하여, 객체 간의 상호작용을 통해 동작하는 프로그래밍 패러다임이다. OOP는 프로그램을 더 이해하기 쉽고 유지보수하기 좋게 만드는 것을 목표로 한다. OOP의 주요 개념에는 클래스, 객체, 속성, 메서드가 있으며, 주요 원칙으로는 캡슐화, 상속, 다형성, 추상화가 있다. 각각의 개념과 원칙은 코드의 재사용성, 유연성, 유지보수성을 높이는 데 기여한다.

## 주요 개념

```js
class Car {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
    this.speed = 0;
  }

  startEngine() {
    console.log(`${this.make} ${this.model}의 엔진이 켜졌습니다.`);
  }

  stopEngine() {
    console.log(`${this.make} ${this.model}의 엔진이 꺼졌습니다.`);
  }

  accelerate(amount) {
    this.speed += amount;
    console.log(
      `${this.make} ${this.model}의 속도가 ${this.speed}로 증가했습니다.`
    );
  }

  brake(amount) {
    this.speed = Math.max(0, this.speed - amount);
    console.log(
      `${this.make} ${this.model}의 속도가 ${this.speed}로 감소했습니다.`
    );
  }
}
```

### 클래스(Class)

클래스는 객체를 생성하기 위한 템플릿이다. 클래스는 객체의 속성(데이터)과 메서드(기능)를 정의한다. 예를 들어, `Car` 클래스는 자동차의 속성(예: 색상, 모델)과 메서드(예: 운전, 멈추기)를 정의할 수 있다.

### 객체(Object)

객체는 클래스의 인스턴스이다. 객체는 클래스에서 정의된 속성과 메서드를 실제 값으로 가지고 있다. 예를 들어, `Car` 클래스의 객체인 `myCar`는 특정 자동차를 나타낸다.

```js
const myCar = new Car("Toyota", "Camry", 2020);
myCar.startEngine(); // Toyota Camry의 엔진이 켜졌습니다.
```

### 속성(Properties)

속성은 객체의 상태를 나타내는 변수이다. 클래스 내에서 정의되며, 객체마다 고유한 값을 가질 수 있다. 예를 들어, `make`, `model`, `year`는 `Car` 클래스의 속성이다.

### 메서드(Methods)

메서드는 객체가 수행할 수 있는 동작이나 기능을 정의하는 함수이다. 클래스 내에서 정의되며, 객체의 상태를 변경하거나 특정 작업을 수행한다. 예를 들어 `startEngine`, `accelerate`는 `Car` 클래스의 메서드이다.

## 주요 원칙

### 캡슐화(Encapsulation)

객체는 자신의 데이터를 보호하기 위해 데이터와 메서드를 하나로 묶어 감춘다. 외부에서는 객체의 내부 상태에 직접 접근할 수 없고, 객체가 제공하는 메서드를 통해서만 접근할 수 있다. 이를 통해 객체의 데이터를 보호하고, 데이터의 무결성을 유지할 수 있다. 또한 캡슐화를 통해 클래스와 객체를 모듈화하여 재사용성을 높일 수 있다.

자바스크립트에서는 캡슐화를 구현하기 위해 프라이빗 변수(private variable), 접근자 메서드(accessor methods), 클래스 필드(private class field), 게터(getter), 세터(setter) 메서드를 활용하여 캡슐화를 구현 할 수 있다.

> 프라이빗 변수: 외부에서 직접 접근할 수 없는 변수
> 게터 메서드(getter method): 프라이빗 변수의 값을 읽기 위한 메서드
> 세터 메서드(setter method): 프라이빗 변수의 값을 설정하기 위한 메서드

#### 기본 클래스 정의

Car 클래스를 정의한다. 여기서는 `_speed`라는 프라이빗 변수를 사용하고, `get speed()`와 `set speed()`를 통해 접근할 수 있도록 한다.

```js
class Car {
  constructor(make, model, year) {
    this.make = make; // 제조사
    this.model = model; // 모델
    this.year = year; // 연도
    this._speed = 0; // 프라이빗 변수로 사용
  }

  startEngine() {
    console.log(`${this.make} ${this.model}의 엔진이 켜졌습니다.`);
  }

  stopEngine() {
    console.log(`${this.make} ${this.model}의 엔진이 꺼졌습니다.`);
  }

  accelerate(amount) {
    this._speed += amount;
    console.log(
      `${this.make} ${this.model}의 속도가 ${this._speed}로 증가했습니다.`
    );
  }

  brake(amount) {
    this._speed = Math.max(0, this._speed - amount);
    console.log(
      `${this.make} ${this.model}의 속도가 ${this._speed}로 감소했습니다.`
    );
  }

  // 게터 메서드
  get speed() {
    return this._speed;
  }

  // 세터 메서드
  set speed(value) {
    if (value < 0) {
      console.log("속도는 음수가 될 수 없습니다.");
    } else {
      this._speed = value;
    }
  }
}
```

#### 객체 생성 및 사용

`Car` 객체를 생성하고, 프라이빗 변수 `_speed`에 접근할 때 게터와 세터를 사용한다.

```js
const myCar = new Car("Toyota", "Camry", 2020);

// 엔진을 켜기
myCar.startEngine(); // Toyota Camry의 엔진이 켜졌습니다.

// 속도를 증가시키기
myCar.accelerate(20); // Toyota Camry의 속도가 20로 증가했습니다.

// 현재 속도 출력 (게터 사용)
console.log(myCar.speed); // 20

// 속도를 줄이기
myCar.brake(5); // Toyota Camry의 속도가 15로 감소했습니다.

// 현재 속도 출력 (게터 사용)
console.log(myCar.speed); // 15

// 세터를 사용해 속도 설정
myCar.speed = 50; // 속도를 50으로 설정
console.log(myCar.speed); // 50

// 잘못된 속도 설정 시도
myCar.speed = -10; // 속도는 음수가 될 수 없습니다.
console.log(myCar.speed); // 50 (변경되지 않음)
```

> 게터 메서드는 객체의 프라이빗 변수 값을 읽을 수 있도록 한다. `get` 키워드를 사용하여 정의된다.
> 세터 메서드는 객체의 프라이빗 변수 값을 설정할 수 있도록 한다. `set` 키워드를 사용하여 정의된다.

`_speed` 변수는 외부에서 직접 접근할 수 없으며, 오직 `get speed()`와 `set speed(value)` 메서드를 통해서만 접근할 수 있다. 이를 통해 `speed` 값이 음수가 되지 않도록 검증할 수 있다.

### 상속(Inheritance)

상속은 기존 클래스를 바탕으로 새로운 클래스를 생성하는 방법이다. 새로운 클래스(자식 클래스)는 기존 클래스(부모 클래스)의 속성과 메서드를 상속받아 재사용할 수 있다. 상속을 통해 코드의 재사용성과 확장성을 높일 수 있다. 예를 들어 `ElectricCar` 클래스는 `Car` 클래스를 상속받아 배터리 관련 속성과 메서드를 추가할 수 있다.

```js
class ElectricCar extends Car {
  constructor(make, model, year, batteryCapacity) {
    super(make, model, year);
    this.batteryCapacity = batteryCapacity;
  }

  chargeBattery() {
    console.log(`${this.make} ${this.model}의 배터리가 충전 중입니다.`);
  }
}

const myElectricCar = new ElectricCar("Tesla", "Model S", 2022, "100kWh");
myElectricCar.startEngine(); // Tesla Model S의 엔진이 켜졌습니다.
myElectricCar.chargeBattery(); // Tesla Model S의 배터리가 충전 중입니다.
```

#### 다중 상속(Multiple Inheritance)

다중 상속은 하나의 클래스가 여러 부모 클래스를 상속받는 기능을 말한다. 복잡성과 충돌 문제를 일으킬 수 있기 때문에 자바스크립트는 다중 상속을 직접 지원하지 않는다.

### 다형성(Polymorphism)

다형성은 하나의 인터페이스나 메서드가 다양한 형태를 가질 수 있는 특성을 의미한다. 같은 이름의 메서드가 다른 클래스에서 다르게 구현 될 수 있다. 다형성은 코드의 유연성과 확장성을 높여 주며, 객체를 보다 일반적이고 재사용 가능하게 만드는 데 큰 역할을 한다. 예를 들어 `Car` 클래스와 `ElectricCar` 클래스 모두 `startEngine` 메서드를 가질 수 있지만, 구현 방식이 다를 수 있다.

```js
class Car {
  // ... 기존 코드 생략
  startEngine() {
    console.log(`${this.make} ${this.model}의 엔진이 켜졌습니다.`);
  }
}

class ElectricCar extends Car {
  // ... 기존 코드 생략
  startEngine() {
    console.log(`${this.make} ${this.model}의 전기 모터가 켜졌습니다.`);
  }
}

const myCar = new Car("Toyota", "Camry", 2020);
const myElectricCar = new ElectricCar("Tesla", "Model S", 2022, "100kWh");

myCar.startEngine(); // Toyota Camry의 엔진이 켜졌습니다.
myElectricCar.startEngine(); // Tesla Model S의 전기 모터가 켜졌습니다.
```

#### 메서드 오버라이딩(Method Overriding)

메서드 오버라이딩은 자식 클래스가 부모 클래스의 메서드를 재정의하여 사용하는 것이다. 이를 통해 자식 클래스는 부모 클래스의 메서드를 자신의 방식으로 구현할 수 있다.

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a sound.`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks.`);
  }
}

class Cat extends Animal {
  speak() {
    console.log(`${this.name} meows.`);
  }
}

const dog = new Dog("Rex");
const cat = new Cat("Whiskers");

dog.speak(); // Rex barks.
cat.speak(); // Whiskers meows.
```

#### 메서드 오버로딩(Method Overloading)

메서드 오버로딩은 같은 이름의 메서드를 여러 개 정의하고, 매개변수의 유형이나 개수에 따라 다른 방식으로 동작하게 하는 것이다. 자바스크립트에서 직접 지원하지 않지만 조건문을 사용하여 유사한 기능을 구현할 수 있다.

```js
class Calculator {
  add(a, b) {
    if (typeof a === "number" && typeof b === "number") {
      return a + b;
    } else if (
      Array.isArray(a) &&
      a.length === 2 &&
      Array.isArray(b) &&
      b.length === 2
    ) {
      return [a[0] + b[0], a[1] + b[1]];
    } else {
      throw new Error("Invalid arguments");
    }
  }
}

const calc = new Calculator();

console.log(calc.add(1, 2)); // 3
console.log(calc.add([1, 2], [3, 4])); // [4, 6]
```

### 추상화(Abstraction)

추상화는 복잡한 시스템에서 중요한 부분만을 모델링하여 간단하게 표현하는 방법이다. 불필요한 세부 사항을 숨기고 중요한 기능에만 집중할 수 있게 한다. 쉽게 말해서 구체적인 세부 사항을 숨기고, 꼭 필요한 부분만을 드러내는 것이다. 예를 들어, 운전자는 자동차의 엔진 내부 구조를 알 필요 없이 운전만 할 수 있으면 되는 것이다. 추상화를 통하여 코드의 간결화, 유지보수 용이, 코드 재사용성, 설계의 명확성 등의 장점을 얻을 수 있다.

#### 데이터 추상화(Data Abstraction)

데이터 추상화는 객체의 속성, 즉 데이터를 다루는 방식이다. 클래스 설계를 통해 공통 속성과 기능을 정의하는 것이다. 데이터 추상화는 복잡한 데이터를 간단한 구조로 나타내는 방법이다. 예를 들어, `Car` 클래스는 자동차의 공통 속성과 기능을 정의한다. 다양한 자동차 객체들이 공유할 수 있는 공통된 인터페이스를 제공한다.

```js
class Car {
  constructor(make, model, year) {
    this.make = make; // 제조사
    this.model = model; // 모델
    this.year = year; // 연도
  }

  startEngine() {
    console.log(`${this.make} ${this.model}의 엔진이 켜졌습니다.`);
  }

  stopEngine() {
    console.log(`${this.make} ${this.model}의 엔진이 꺼졌습니다.`);
  }
}

const myCar = new Car("Toyota", "Camry", 2020);
myCar.startEngine(); // Toyota Camry의 엔진이 켜졌습니다.
myCar.stopEngine(); // Toyota Camry의 엔진이 꺼졌습니다.
```

#### 행동 추상화(Behavior abStraction)

행동 추상화는 객체의 메서드, 즉 동작을 다루는 방식이다. 추상 클래스와 추상 메서드는 이러한 행동 추상화를 구현하는 도구이다. 추상 클래스는 구현되지 않은 메서드를 정의하고, 이를 상속받은 클래스들이 해당 메서드를 구현하도록 강제한다. 예를 들어, `Animal` 클래스는 추상 클래스이다. `speak` 메서드는 구현되지 않았으며, 자식 클래스에서 반드시 구현해야 한다.

```js
class Animal {
  constructor(name) {
    if (new.target === Animal) {
      throw new Error("Cannot instantiate abstract class.");
    }
    this.name = name;
  }

  speak() {
    throw new Error('Method "speak()" must be implemented.');
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks.`);
  }
}

const myDog = new Dog("Rex");
myDog.speak(); // Rex barks.

// const animal = new Animal('Generic'); // Error: Cannot instantiate abstract class.
```
