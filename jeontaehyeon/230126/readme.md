## Day6

#### <a href="https://ko.javascript.info/date#ref-2097">Date 객체와 날짜</a>
링크를 참조.
***
#### JSON 과 Method
네트워크를 통해 데이터를 주고받을 때 객체를 문자열로 전환하여야 하고 이것은 아주 번거로운 작업이다.
이를 예방하기 위해 JSON을 사용한다.
JSON에서 제공하는 method는 다음과 같다.
`JSON.stringify` – 객체를 JSON으로 바꿈

`JSON.parse` – JSON을 객체로 바꿈.


```javascript
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  wife: null
};
let json = JSON.stringify(student);

alert(typeof json); // type이 문자열로 바뀜

alert(json);
/* JSON으로 인코딩된 객체:
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "wife": null
}
*/
```
이렇게 변경된 문자열은 JSON으로 인코딩된(JSON-encoded), 직렬화 처리된(serialized), 문자열로 변환된(stringified), 결집된(marshalled) 객체라고 부른다.
JSON에서는 백틱이나 작은 따옴표를 사용할 수 없으므로 이에 주의해야한다.
JSON.stringify는 객체, 배열, 문자형 ,숫자형, 불린형에 사용할 수 있다.

만약 함수, 심볼, 혹은 undefined인 프로퍼티가 존재한다면 그 값은 무시된다.


```javascript
let user = {
  sayHi() { // 무시
    alert("Hello");
  },
  [Symbol("id")]: 123, // 무시
  something: undefined // 무시
};

alert( JSON.stringify(user) ); // {} (빈 객체가 출력됨)
```
만약 객체가 서로 순환참조를 할 경우에는 에러가 발생한다.
```javascript
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  participants: ["john", "ann"]
};

meetup.place = room;
room.occupiedBy = meetup;
gify(meetup); // Error: Converting circular structure to JSON
```
이런 상황을 방지할 수 있는 방법으로 replacer을 사용할 수 있다.

```javascript
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  participants: [{name: "John"}, {name: "Alice"}],
  place: room // meetup references room
};
room.occupiedBy = meetup; // room references meetup

alert( JSON.stringify(meetup, ['title', 'participants', 'place', 'name', 'number']) );
/*
{
  "title":"Conference",
  "participants":[{"name":"John"},{"name":"Alice"}],
  "place":{"number":23}
}
*/
```
<a href="https://ko.javascript.info/json#ref-2060">링크</a>를 참고하면 replacer에 대한 더 많은 기능을 확인할 수 있다.

또한 space method를 사용하여 가독성을 높이는 것도 가능하다
```javascript
alert(JSON.stringify(user, null, 2));
/* 공백 문자 두 개를 사용하여 들여쓰기함:
{
  "name": "John",
  "age": 25,
  "roles": {
    "isAdmin": false,
    "isEditor": true
  }
}
*/

/* JSON.stringify(user, null, 4)라면 아래와 같이 좀 더 들여써집니다.
{
    "name": "John",
    "age": 25,
    "roles": {
        "isAdmin": false,
        "isEditor": true
    }
}
*/
```

stringify함수는 toJSON method를 정의하여 커스터마이징 할 수 있다.

```javascript
let room = {
  number: 23,
  toJSON() {
    return this.number;
  }
};

let meetup = {
  title: "Conference",
  room
};

alert( JSON.stringify(room) ); // 23

alert( JSON.stringify(meetup) );
/*
  {
    "title":"Conference",
    "room": 23
  }
*/
```

JSON.parse를 사용하면 반대로 JSON 객체를 객체로 디코딩 할 수 있다.
```javascript
// 문자열로 변환된 배열
let numbers = "[0, 1, 2, 3]";

numbers = JSON.parse(numbers);

alert( numbers[1] ); // 1
```

<a href="https://ko.javascript.info/json#ref-2064"> reviver</a>에 대한 정보는 여기


