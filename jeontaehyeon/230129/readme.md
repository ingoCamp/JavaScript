## Day7

#### 나머지 매개변수와 스프레드 문법
```javascript
function showName(firstName, lastName, ...titles) {
  alert( firstName + ' ' + lastName ); // Bora Lee
  // 나머지 인수들은 배열 titles의 요소
  // titles = ["Software Engineer", "Researcher"]
  alert( titles[0] ); // Software Engineer
  alert( titles[1] ); // Researcher
  alert( titles.length ); // 2
}

showName("Bora", "Lee", "Software Engineer", "Researcher");
```
나머지 매개변수는 항상 마지막에 위치해야 함

arguments 객체
```javascript
function showName() {
  alert( arguments.length );
  alert( arguments[0] );
  alert( arguments[1] );

  // arguments는 이터러블 객체이기 때문에
  // for(let arg of arguments) alert(arg); 를 사용해 인수를 펼칠 수 있다
}
// 2, Bora, Lee가 출력됨
showName("Bora", "Lee");
// 1, Bora, undefined가 출력됨(두 번째 인수는 없음)
showName("Bora");
```
parameter를 설정하지 않아도 arguments로 접근 가능
***
#### 스프레드 문법
Math.max와 같은 스프레드 문법에 배열을 넘겨줄 때
```javascript
let arr = [3, 5, 1];
alert( Math.max(arr) ); // NaN
```
위와 같이 넘겨주면 에러가 발생한다.

```javascript
let arr = [3, 5, 1];

alert( Math.max(...arr) ); // 5 (스프레드 문법이 배열을 인수 목록으로.)
```
위와같이 나머지를 사용

***
#### 기명함수 표기법
```javascript
let sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    func("Guest"); 
  }
};
let welcome = sayHi;
sayHi = null;
welcome(); // Hello, Guest (중첩 호출이 제대로 동작함)
```
위 코드의 인자로 "man"을 넘겨주면 Hello, man이 출력됨
***
#### new Function
```javascript
let str = ... 서버에서 동적으로 전달받은 문자열(코드 형태) ...

let func = new Function(str);
func();
```
new Function을 사용하면 런타임에서 인자를 받아 동적으로 컴파일 해야하는 경우에 쓰일 수 있다. 이때  new Function을 이용해 만든 함수는 외부 변수에 접근할 수 없고, 오직 전역 변수에만 접근할 수 있다. 
```javascript
function getFunc() {
  let value = "test";

  let func = new Function('alert(value)');

  return func;
}

getFunc()(); // ReferenceError: value is not defined
```
즉 위와 같은 코드에서 에러가 발생

***
#### 콜백
loadScript와 같은 함수는 비동기적으로 실행되기 때문에  loadScript아래에 있는 코드들은 스크립트 로딩이 종료되는 것을 기다리지 않는다.
따라서 아래와 같이 콜백함수를 사용할 필요가 있다.
```javascript
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(script);

  document.head.append(script);
}
```
```javascript
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;
  script.onload = () => callback(script);
  document.head.append(script);
}

loadScript('https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js', script => {
  alert(`${script.src}가 로드되었습니다.`);
  alert( _ ); // 스크립트에 정의된 함수
});
```
콜백함수의 에러핸들링 위해 첫번재 인자는 남겨두는 것이 관례이다. 
또한 코드를 구성할 때 <a href="https://ko.javascript.info/callbacks#ref-86">멸망의 피라미드</a>를 피할 수 있도록 구성하도록 해야한다.

