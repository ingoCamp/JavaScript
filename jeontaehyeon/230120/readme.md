## Day2

#### 화살표 함수 기본

화살표 함수는 본문이 한 줄인 함수를 작성할 때 유용. 본문이 한 줄이 아니라면 다른 방법으로 화살표 함수를 작성해야 함
이때는 return을 반드시 포함할 수 있도록 해야한다.

```javascript
let sum=(a,b)=>a+b;
//한줄일 때

let  sum  =  (a, b)  =>  {
	let result = a+b
	return result;
};
//여러 줄로 선언했을 때에는 return해주기
```


***

#### 객체
객체는 중괄호를 이용하여 만들 수 있고, key, value로 구성된 property를 여러개 넣을 수 있다.
key에는  문자형, value에는 모든 자료형이 허용된다.
```javascript
let user= new Object();//객체 생성자 문법
let user = {}//객체 리터럴 문법
```
***
#### 리터럴과 프로퍼티


```javascript
let user =  {  // 객체
 name:  "John",  // 키: "name", 값: "John"
 age:  30  // 키: "age", 값: 30
"likes birds":  true


user["likes birds"]  =  true;
delete user["likes birds"];

};
```

 colon을 기준으로 왼쪽엔 key, 오른쪽에는 value가 위치한다.

문장은 세미콜론으로 구별한다, 줄바꿈이 있으면 생략가능

복수의 단어가 있다면 ""로 묶어줘야 한다.

복수의 단어로 선언한 프로퍼티 키의 경우에는 점 표기법을 이용해 프로퍼티의 값을 읽을 수 없다.
***
#### 계산된 프로퍼티
리터럴 안의 프로퍼티 키가 대괄호로 묶여있는 경우 이를 계산된 프로퍼티라고 부른다. 
```javascript
let fruit =  prompt("어떤 과일을 구매하시겠습니까?",  "apple");
let bag =  {
	[fruit]: 5,
};
alert( bag.apple );
```
prompt에 apple입력시 bag에 "apple" property key를 갖는 property가 생성됨.
***
#### in 연산자
in 연산자로 property의 존재여부를 확인할 수 있다.

```javascript
"key"  in object//형태의 문법

for  (key in object)  {}
```
for와 in을 사용하면 객체의 모든 키를 순회할 수 있다.

***
#### 객체 정렬 방식
`integer property` 인 경우 자동으로 정렬되고 아닌 경우는 추가된 순서로 정렬된다.
***
#### 참조에 의한 비교
```javascript
let a = {};

let b = a; // 참조에 의한 복사

  

alert( a == b ); // true, 두 변수는 같은 객체를 참조합니다.

alert( a === b ); // true
//---------------------------------//

let a = {};

let b = {}; // 독립된 두 객체

  

alert( a == b ); // false
```


***
#### 객체 복사, 병합과 Object 
기존에 있던 객체와 똑같지만 독립적인 객체를 만들고 싶을 땐?
- 프로퍼티들을 순회해 원시 수준까지 프로퍼티를 복사
- assign사용
```javascript
let user = {

name: "John",

age: 30

};

let clone = {}; 


for (let key in user) {

clone[key] = user[key];

}
```

위 예제는 순회하여 사용한 것이다.
```javascript
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

Object.assign(user, permissions1, permissions2);

// now user = { name: "John", canView: true, canEdit: true }
```
assign을 사용하여 독립적인 객체를 생성한 것이다.
만약 동일한 이름을 가진 property가 있다면 기존 값이 업데이트 된다.

```javascript

let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};
```
위와 같이 객체안에 객체가 들어있는 형태에서는 deep cloning이 필요하다.
