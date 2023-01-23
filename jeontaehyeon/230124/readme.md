## Day4

#### iterable 객체
iterable 객체는 배열을 일반화한 객체이다.

```javascript
let range = {
  from: 1,
  to: 5
};
```
위와 같은 코드는 for..of를 적용하기 적합하지 않다
range를 iterable로 만들려면 특수내장 심볼인 `Symbol.iterator` method를 사용추가해야 한다.
```javascript
let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```
동작하는 순서는 위 코드와 같다. 시작하는 값(끝 값)을 정해주고, next에 동작 형태를 next에 지정해준다.
range 객체에는 next()가 없기 때문에 range[Symbol.iterator]\()를 호출하여 안에 정의된 next()를 사용한다.
`문자열도 iterable이다.`

iterator를 명시적으로 호출하면 `for..of`를 사용했을 때보다 반복과정을 제어하기가 쉽다는 장점이 있다.
```javascript
let str = "Hello";

// for..of를 사용한 것과 동일한 작업을 합니다.
// for (let char of str) alert(char);

let iterator = str[Symbol.iterator]();

while (true) {
  let result = iterator.next();
  if (result.done) break;
  alert(result.value); // 글자가 하나씩 출력됩니다.
}
```
iterable(Symbol.iterator가 구현된 객체)이나 유사 배열(index와 length가 있어 배열처럼 보이는 객체)는 서로 다른 것이고 실제 배열이 아니기 때문에 배열 method를 지원하지 않는다.
이것을 진짜 배열로 만들어주는 범용method가 있다.`Array.from`

```javascript
// range는 챕터 위쪽 예시에서 그대로 가져왔다고 가정합시다.
let arr = Array.from(range);
alert(arr); // 1,2,3,4,5 (배열-문자열 형 변환이 제대로 동작합니다.)
```
 mapFn와 thisArg는 각 요소에 함수를 적용할 수 있게 해준다.
***
#### 맵과 셋
맵은 키가 있는 객체를 저장한다는 점에서 객체와 유사하지만 키에 다양한 자료형을 허용한다는 차이점이 있다.
맵은 아래와 같은 method와 property가 있다.
`new Map()` – 맵을 만든다.
`map.set(key, value)` – key를 이용해 value를 저장.
`map.get(key)` – key에 해당하는 값을 반환,.key가 존재하지 않으면 undefined를 반환.
`map.has(key)` – key가 존재하면 true, 존재하지 않으면 false를 반환.
`map.delete(key)` – key에 해당하는 값을 삭제.
`map.clear()` – 맵 안의 모든 요소를 제거.
`map.size` – 요소의 개수를 반환.

```javascript
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("보라");

alert(user.name); // 보라
alert(user.isAdmin); // falselet map = new Map();

map.set('1', 'str1');   // 문자형 키
map.set(1, 'num1');     // 숫자형 키
map.set(true, 'bool1'); // 불린형 키
alert( map.get(1)   ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```
객체는 key값을 문자열로 저장했지만 map의 경우에는 자료형 그대로를 저장하는 것을 확인할 수 있다.

생성자 내에 method를 선언하여 유연성을 확보할 수 있다.
> map[key]는 Map을 쓰는 바른 방법이 아니다
map[key] = 2로 값을 설정하는 것 같이 map[key]를 사용할 수 있긴 하지만. 하지만 이 방법은 map을 일반 객체처럼 취급하게 된다. map을 사용할 땐 map전용 메서드 set, get 등을 사용하는 것이 좋다.

`맵은 객체를 키로 사용할 수 있다.`

```javascript
let john = { name: "John" };

// 고객의 가게 방문 횟수를 세본다고 가정해 봅시다.
let visitsCountMap = new Map();

// john을 맵의 키로 사용하겠습니다.
visitsCountMap.set(john, 123);

alert( visitsCountMap.get(john) ); // 123
```
map.set은 호출할 때마다 자신이 호출되기 때문에 체이닝이 가능하다
```javascript
map.set('1', 'str1')
  .set(1, 'num1')
  .set(true, 'bool1');
```
맵의 요소에는 아래와 같은 method를 사용하여 반복작업을 용이하게 할 수 있다.
`map.keys()` – 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환.
`map.values()` – 각 요소의 값을 모은 이터러블 객체를 반환
`map.entries()` – 요소의 [키, 값]을 한 쌍으로 하는 이터러블 객체를 반환.

```javascript
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',    50]
]);

// 키(vegetable)를 대상으로 순회합니다.
for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

// 값(amount)을 대상으로 순회합니다.
for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

// [키, 값] 쌍을 대상으로 순회합니다.
for (let entry of recipeMap) { // recipeMap.entries()와 동일합니다.
  alert(entry); // cucumber,500 ...
}
```
맵은 삽입된 순서를 기억한다.

객체를 맵으로 바꾸어 맵을 초기화할 수도 있다.
이때 object.entries를 사용할 수 있다.
object.fromEntries를 사용하면 맵을 객체로 만
들 수 있다. 아래 링크 참조
https://ko.javascript.info/map-set#ref-1335
https://ko.javascript.info/map-set#ref-1336

`셋(set)`은 중복을 허용하지 않는 value를 모아놓은 컬렉션이다.

set의 method는 다음과 같다.
`new Set(iterable)` – 셋을 만든다. 이터러블 객체를 전달받으면(대개 배열을 전달받음) 그 안의 값을 복사해 셋에 초기화해준다.
`set.add(value)` – 값을 추가하고 셋 자신을 반환.
`set.delete(value)` – 값을 제거. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 true, 아니면 false를 반환.
`set.has(value)` – 셋 내에 값이 존재하면 true, 아니면 false를 반환.
`set.clear()` – 셋을 비운다.
`set.size` – 셋에 몇 개의 값이 있는지.

동일안 value가 있다면 set에 아무리 많이 호출을 하더라도 반응이 없다.

set값에 반복 작업

```javascript
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// forEach를 사용해도 동일하게 동작합니다.
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```
셋도 추가한 순서대로 
셋에 대한 추가 정보는 아래 링크
https://ko.javascript.info/map-set#ref-1338
***

