## Day3

#### 메서드와 this
자바스크립트에서 객체에 함수를 할당하여 동작할 수 있도록 한다.

```javascript
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
  alert("안녕하세요!");
};

user.sayHi(); // 안녕하세요!
```
이런식으로 객체에 할당된 함수를 method라고 부른다.
```javascript
function sayHi() {
  alert("안녕하세요!");
};

// 선언된 함수를 메서드로 등록
user.sayHi = sayHi;

user.sayHi(); // 안녕하세요!
```
다음과 같이 이미 정의된 함수를 사용하여 method를 정의할 수 있다.

```javascript
user = {
  sayHi: function() {
    alert("Hello");
  }
};
user = {
  sayHi() { // "sayHi: function()"과 동일
    alert("Hello");
  }
};
```
위와같이 단축 구문을 사용하여 정의할 수 있다.

대부분의 method가 객체 프로퍼티의 값을 사용한다 이때 this 키워드를 사용할 수 있다.

this는 메서드를 호출할 때 사용된 객체를 나타낸다.
```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // 'this'는 '현재 객체'를 나타냅니다.
    alert(this.name);
  }

};

user.sayHi(); // John
```
this를 사용하지 않고 외부 변수를 사용하여 참조할 수도 있지만 이러할 경우 객체가 다른 값으로 덮혀졌을 때 error가 발생할 수 있다.

`자바 스크립트의 모든 함수에서 this를 사용할 수 있다.` 
```javascript
function sayHi() {
  alert( this.name );
}let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// 별개의 객체에서 동일한 함수를 사용함
user.f = sayHi;
admin.f = sayHi;

// 'this'는 '점(.) 앞의' 객체를 참조하기 때문에
// this 값이 달라짐
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)
```
이러한 자유로운 this 때문에 주의하여야 한다.

arrow function의 경우 고유한 this를 가지지 않는다.

```javascript
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라
```
따라서 arrow의 this가 아니라 sayHi의 this를 사용하게 된다.
***
#### new연산자와 생성자 함수
유사한 객체를 여러개 만들어야 될 때는 어떻게 해야할까? ->new 연산자와 함께 생성자를  사용하여 해결할 수 있다.
```javascript
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("보라");

alert(user.name); // 보라
alert(user.isAdmin); // false
```
위와 같이 new연산자와 함께 user을 정의하였을 때 User와 동일한 프로퍼티를 같는 객체를 얻을 수 있다. 

target, return에대한 추가정보는
https://ko.javascript.info/constructor-new

생성자 내에 method를 선언하여 유연성을 확보할 수 있다.
```javascript
function User(name) {
  this.name = name;

  this.sayHi = function() {
    alert( "제 이름은 " + this.name + "입니다." );
  };
}

let bora = new User("이보라");

bora.sayHi(); // 제 이름은 이보라입니다.

/*
bora = {
   name: "이보라",
   sayHi: function() { ... }
}
*/
```
***
#### 원시값의 메서드
자바스크립트에서는 원시값을 마치 객체처럼 다를 수 있다. 즉 원시값에서도 객체에서처럼 메서드를 호출할 수 있다.
```javascript
let str = "Hello";

alert( str.toUpperCase() ); // HELLO
```
위와 값이 string 원시값에서 method를 호출하는 순간 Hello라는 문자열의 값을 알고 있고 toUpperCase라는 함수를 가진 객체가 생성된다. 이때 method가 실행되고, 객체는 파괴되고 원시값만 남게된다.

***
#### 문자열
자바에서는 글자 하나만 저장할 수 있는 별도의 자료형은 없다
`''`나 `""`는 기능적으로 차이가 없지만 , 백틱은 특별한 기능을 가진다.
```javascript
function sum(a, b) {
  return a + b;
}

alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3.
```
위와 같이 `${}`문법에 넣어 사용하면 쉽게 문자열 중간에 표현식을 사용할 수 있다.
```javascript
let guestList = `손님:
 * John
 * Pete
 * Mary
`;
```
다음과 같이 여러줄에 표현할 때에도 백틱을 사용할 수 있다.

`문자열의 길이를 나타내는 length는 함수가 아니라 프로퍼티이기 때문에 ()를 붙여 사용하지 않는다.`

문자열은 불변성을 가지기 때문에 하나만 수정할 수는 없다.
```javascript
let str = 'Hi';

str[0] = 'h'; // Error: Cannot assign to read only property '0' of string 'Hi'
alert( str[0] ); // 동작하지 않습니다.
```
즉 위와같이 하나의 문자만 수정할 수는 없음 (문자열 전체를 변경하는건 가능)
이외에 추가적인 문자열 method, 프로퍼티는 
https://ko.javascript.info/string
참고
***
