## 자바스크립트란?
---
> <b>정의</b>
웹 페이지에 생동감을 불어넣기 위해 만들어진 프로그래밍 언어.

- 자바스크립트로 작성한 프로그램을 "스크립트(script)" 라고 부른다.
웹페이지에서 HTML에 작성되는데, 웹페이지를 불러올 때 스크립트가 자동으로 실행되게 된다.

---

> <b>왜 자바스크립트?</b>
원래 처음 이름은 liveScript였는데, java의 인기가 매우 좋을 때라 홍보하기 좋을 거 같아 "자바스크립트"라고 이름지었다.

---

> <b>자바스크립트의 실행</b>
자바스크립트는 브라우저, 서버 모두에서 실행 할 수 있다.
- **자바스크립트 엔진**이라는 프로그램이 있는 모든 곳에서 동작한다.
- 브라우저에 **"자바스크립트 가상 머신"** 이라고 불리는 엔진이 내장되어 있다.
    - Chrome과 Opera에서 쓰이는 'V8'
    - Firefox에서 씌는 'SpiderMonkey'

---

> <b>엔진 동작 원리</b>
1. 엔진이 스크립트를 읽는다. (파싱)
2. 읽어들인 스크립트를 기계어로 전환한다. (컴파일)
3. 전환한 코드가 실행된다.

---

> <b>자바스크립트에서 가능한 일</b>
- HTML수정, 추가
- 사용자 행동에 반응 (마우스, 키포드 등)
- 서버에 요청 보내기, 파일 다운 받기, 업로드 하기 등
- 쿠키 가져오거나 설정하기
- 로컬스토리지를 이용하여 클라이언트 측에 데이터 저장하기.

---

> <b>자바스크립트에서 불가능한 일</b>
- **메모리나 CPU같은 저수준 영역의 조작이 허용되지 않는다.**
- 디스크에 저장된 파일을 읽거나 쓸때 제약이 있을 수 있다. 
- 운영체제의 기능을 브라우저가 직접 사용하지 못하게 제한이 걸려 있기 때문이다.
- 카메라나 마이크와 상호작용을 하려면 명시적 허가가 필요하다.
- 브라우저 내의 다른 탭 사이에 정보는 공유되지 않는다. 다른 사이트가 특정 사이트의 정보를 훔치는 것을 방지하기 위함이다.
- 어떤 창에서 다른 창이 열리는 경우에 예외가 있을 수 있다. 그러나,
- **`동일 출처 정책`** : 도메인이나 프로토콜, 포트가 다르면 어떤 창에서 다른 창을 열어도 정보가 공유되지 않고 접근 할 수 없다.

---

><b>자바스크립트만의 강점</b>
- HTML과 CSS를 완전히 통합할 수 있다.
- 간단한 일은 간단하게 처리할 수 있다.
- 모든 주요 브라우저에서 지원하고 기본 언어로 사용되고 있다.

---

> 자바스크립트 너머의 언어들

다른 언어들이 자바스크립트로 트랜스파일 되어 사용되기도 한다
ex) CoffeeScript, TypeScript, Flow, Dart 등