﻿## Day5

#### 구조 분해 할당
객체나 배열을 변수로 분해할 수 있는 문법
```javascript
// 이름과 성을 요소로 가진 배열
let arr = ["Bora", "Lee"]
// firstName엔 arr[0]을
// surname엔 arr[1]을 할당
let [firstName, surname] = arr;

alert(firstName); // Bora
alert(surname);  // Lee
};
```
Index로 접근하지 않고 변수를 선언하여 접근가능,
split같이 반환형이 배열인 method를 사용할 수도 있다.
```javascript
let [firstName, surname] = "Bora Lee".split(' ');
```
```javascript
let [firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

alert( title ); // Consul
```

```javascript
let [a, b, c] = "abc"; // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3]);
```
또한 할당 연산자 옆에는 모든 iterable이 올 수 있다. 문자열은 iterable하기 때문에 구조 분해 할당을 적용할 수 있다.

```javascript
let user = {};
[user.name, user.surname] = "Bora Lee".split(' ');
alert(user.name); // Bora
```
위 코드와 같이 객체 프로퍼티도 할당 연산자의 왼쪽에 위치할 수 있다.
 mapFn와 thisArg는 각 요소에 함수를 적용할 수 있게 해준다.
```javascript
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

alert(name1); // Julius
alert(name2); // Caesar

// `rest`는 배열입니다.
alert(rest[0]); // Consul
alert(rest[1]); // of the Roman Republic
alert(rest.length); // 2
```
위와 같이 ...을 사용하면 나머지 값들을 한번에 받을 수 있다.

```javascript
let [name = "Guest", surname = "Anonymous"] = ["Julius"];

alert(name);    // Julius (배열에서 받아온 값)
alert(surname); // Anonymous (기본값)
```
위와 같이 default 값을 정해줄 수도 있다.

```javascript
let [surname = prompt('성을 입력하세요.'), name = prompt('이름을 입력하세요.')] = ["김"];

alert(surname); // 김 (배열에서 받아온 값)
alert(name);    // prompt에서 받아온 값
```
또한 함수를 이용하여 값을 받아올 수도 있다. 이때 값이 제공되지 않았을 때만 함수가 호출되기 때문에 prompt는 한번만 호출될 것이다.
***
#### 중첩 구조 분해
```javascript
let options = {
  size: {
    width: 100,
    height: 200
  },
  items: ["Cake", "Donut"],
  extra: true
};

// 코드를 여러 줄에 걸쳐 작성해 의도하는 바를 명확히 드러냄
let {
  size: { // size는 여기,
    width,
    height
  },
  items: [item1, item2], // items는 여기에 할당함
  title = "Menu" // 분해하려는 객체에 title 프로퍼티가 없으므로 기본값을 사용함
} = options;

alert(title);  // Menu
alert(width);  // 100
alert(height); // 200
alert(item1);  // Cake
alert(item2);  // Donut
```
위 코드와 같이 객체 안에 객체나 배열이 복잡하게 얽혀있을 때 복잡한 패턴을 사용하면 중첩 배열이나 객체의 정보를 추출할 수 있다. 이를 중첩 구조 분해라고 한다.


#### 똑똑한 매개변수


```javascript

function showMenu(title = "Untitled", width = 200, height = 100, items = []) {
  // ...
}
showMenu("My Menu", undefined, undefined, ["Item1", "Item2"])
```
위와 같이 함수를 선언하면 매개변수의 순서가 틀리거나, 굳이 전달하지 않아도 되는 매개변수를 전달해야되는 불편함이 있다.

```javascript
let options = {
  title: "My menu",
  items: ["Item1", "Item2"]
};

// 똑똑한 함수는 전달받은 객체를 분해해 변수에 즉시 할당함
function showMenu({title = "Untitled", width = 200, height = 100, items = []}) {
  // title, items – 객체 options에서 가져옴
  // width, height – 기본값
  alert( `${title} ${width} ${height}` ); // My Menu 200 100
  alert( items ); // Item1, Item2
}

showMenu(options);
```
위와 같이 함수를 구성한다면 매개변수로 options를 바로 넘겨줄 수 있다. 즉 전달받은 객체를 분해하여 변수에 즉시 할당한다 .

이때 매개변수를 구조 분해할 때 반드시 인수가 전달된다고 가정되고 사용되기 때문에 아래와 같이 코드를 구성하면 에러를 피할 수 있다.
```javascript
function showMenu({ title = "Menu", width = 100, height = 200 } = {}) {
  alert( `${title} ${width} ${height}` );
}

showMenu(); // Menu 100 200
```
위와 같이 인수 객체의 기본값을 빈 객체{}로 설정하면 에러가 발생하지 않는다.
***


