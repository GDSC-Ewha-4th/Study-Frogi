정리 노션 링크입니다: https://boom-passbook-4e2.notion.site/eef12bf5a2f34b3db899d6b56363ca51?pvs=4

<aside>
1️⃣ **주소창에 www.google.com을 입력하면 일어나는 일은 무엇인가요?**

---

- 대답
    
    사용자가 주소창에 주소를 입력하면 먼저 브라우저가 통신을 위한 ip 주소를 파악하기 시작합니다. 이를 위해 캐싱된 DNS 기록에서 해당 도메인 주소와 대응하는 ip를 계속 탐색하는데요, 브라우저 캐시, OS 캐시, 라우터 캐시, ISP 캐시를 차례대로 확인합니다.
    
    모든 캐시에 요청한 URL이 없는 경우 ISP의 DNS 서버가 DNS recursor로서 recursive search를 통해 해당 도메인 서버의 올바른 ip 주소를 반환합니다.
    
    그리고 통신을 요청하고, 통신 요청에 대한 답을 보내고, 해당 답에 대한 답을 주고받는 3-Way handshaking 과정을 거쳐 브라우저와 서버가 TCP 통신을 시작하게 됩니다. 
    
    이후에는 GET이나 POST 등의 요청을 통해 브라우저가 서버에게 HTTP request를 보냅니다. 해당 요청을 서버가 받으면 request handler가 요청과 요청의 헤더, 쿠키 등을 확인하여 자세한 내용을 확인합니다. 이후 JSON이나 XML 등 특정한 포맷으로 작성한 response를 브라우저에 응답으로 보냅니다.
    
    이를 받은 브라우저는 응답을 파싱하여 콘텐츠를 사용자에게 보여줍니다.
    
</aside>

<aside>
2️⃣ **브라우저 렌더링 원리에 대해서 설명해보세요.**

---

- 대답
    
    브라우저 렌더링 과정은 크게 Construction 과정과 Operation 과정으로 나눌 수 있습니다.
    
    첫 번째로 사용자가 접속하고자 하는 사이트 주소를 입력하면 브라우저가 캐시에서 DNS 기록을 확인하고, 캐시에 기록이 남아있지 않은 경우 recursive search를 통해 해당 도메인의 ip 주소를 찾아냅니다.
    
    해당 ip 주소로 TCP 통신을 시작하게 되면 브라우저가 서버에게 HTTP 통신으로 HTML 파일을 요청합니다. 서버는 그에 따라 HTML 파일을 메모리에 저장하여 바이트 형태로 응답을 보냅니다.
    
    이것을 받은 브라우저는 바이트 형태의 HTML 문서를 문자열로 변환합니다. 그리고 이를 파싱하여 DOM 트리를 생성하게 됩니다. 즉 문자열로 변환된 HTML 문서를 토큰으로 분해하고, 이 토큰을 객체로 변환하여 노드를 생성한 뒤 중첩 관계를 반영하여 트리를 생성하는 것입니다.
    
    이 과정은 동기적으로 이루어지는데요, 중간에 style 태그를 만나면 DOM 생성을 일시 중단하고 HTML과 동일한 파싱 과정을 거쳐 CSSOM 트리를 생성합니다. 트리 생성이 종료되면, HTML 파싱이 중단된 시점으로 돌아가서 다시 HTML 파싱을 진행합니다.
    
    중간에 script 태그가 등장하면 이때도 DOM 생성을 일시 중단하고 script 태그 내 코드를 파싱합니다. 다른 파싱과의 차이점은 렌더링 엔진이 자바스크립트 엔진에게 제어권을 넘기는 블로킹이 발생한다는 점입니다. 소스코드를 토큰으로 분해하고, 이 토큰으로 추상 구문 트리까지 생성이 되면 바이트 코드로 변환한 뒤 인터프리터를 실행시키고, 다시 제어권을 렌더링 엔진으로 넘겨 HTML 파싱을 이어갑니다.
    
    위 과정으로 생성된 DOM 트리와 CSSOM 트리는 합쳐서 브라우저 화면을 페인팅 할 때 쓰이는 렌더 트리를 생성합니다. 여기까지가 Construction 과정이었구요, 이어서 나오는 것이 Operation 과정입니다.
    
    먼저 Render 트리에 있는 노드를 배치하고, 해당 노드의 UI를 그린 뒤 이 노드를 순서대로 구성하면 사용자에게 결과 화면을 출력하게 되면서 Operation 과정을 마무리 짓습니다.
    
</aside>

# 학습 내용

<aside>
⚙ **NodeJS 환경과 브라우저 환경의 차이**

대부분의 프로그래밍 언어는 운영체제(OS)나 가상머신(VM) 위에서 실행된다. 하지만 자바스크립트는 런타임 환경(node.js)에서 실행되지 않는다.

---

**[ 공통점 ]**

- v8엔진이라는 런타임을 통해 돌아간다.
- 공식 자바스크립트 명세(ECMA)를 따른다.

**[ 차이점 ]**

- 전역객체
    - node: global, (파일을 실행하는 경우)Module
    - 브라우저: Window 객체
    
    → node: 브라우저 내장 함수, DOM 활용 시 쓰는 document 객체 사용 ❌
    
    → 브라우저: 파일 시스템 제어(fs), crypto 사용 ❌
    
- 모듈 시스템
    - node: CommonJS → `require()`로 모듈 호출
    - 브라우저: ECMA Script 표준 모듈 → `import`로 모듈 호출

*https://sleepybird.tistory.com/153
*https://velog.io/@shitaikoto/Node.js-browser

</aside>

<aside>
✏️ **브라우저 렌더링 방식을 파악해야하는 이유**

---

- 내가 의도한대로 코드를 실행시키기 위해
- 효율적인 코드를 작성하기 위해
</aside>

*`렌더링`: HTML, CSS, JS로 작성된 문서를 **파싱하여** 브라우저에 시각적으로 **출력**하는 것

# Construction

## 1. 사용자가 브라우저로 웹 사이트에 접속하면 브라우저가 ip 파악

사용자가 주소창에 주소를 입력하면

1. 브라우저는 캐싱된 DNS 기록에서 해당 도메인 주소와 대응하는 IP 주소 확인
    
    *`DNS*Domain Name System*`; URL 이름과 IP 주소를 저장하고 있는 DB
    
    브라우저는 DNS query를 보내 DNS 기록을 아래 4가지 캐시를 순서대로 확인
    
    - 브라우저 캐시: 일정 기간 동안의 DNS 기록 저장
    - OS 캐시: `systemcall`을 통해 OS가 저장하고 있는 DNS 기록에 접근
    - router 캐시: DNS 기록을 캐싱하는 라우터와 통신
    - ISP 캐시
        
        *`ISP`: DNS 서버 구축
        
2. (요청 URL이 캐시에 없을 경우)ISP의 DNS 서버가 recursive search를 통해 해당 도메인 서버의 올바른 ip 주소 반환
    
    *`DNS recursor`; ISP의 DNS 서버. 도메인 이름의 올바른 ip 주소를 찾을 책임 ⭕️
    
    *`name server`; 다른 DNS 서버. 웹사이트 도메인 이름의 구조에 기반하여 검색
    
    *`recursive search`: ip 주소를 찾을 때까지 DNS 서버에서 다른 DNS 서버를 오가며 반복 검색
    
3. 브라우저가 서버와 TCP 통신 시작
    - 3-Way handshaking
    - 웹 사이트의 HTTP 요청은 일반적으로 TCP를 사용한다.

## 2. 브라우저가 서버에게 HTTP Request

- GET/POST 등 요청

## 3. 서버가 브라우저에게 HTTP Response

<aside>
🏙️ 서버는 브라우저가 요청한 내용을 request handler에게 전달한다.

HTML 파일을 읽어들여 메모리에 저장한 다음, 메모리에 저장된 **바이트(2진수)로 응답**한다.

</aside>

<aside>
🦕 브라우저는 응답받은 바이트 형태의 HTML 문서를 meta 태그의 charset 어트리뷰트로 지정해 둔 인코딩 방식(ex.UTF-8)을 기준으로 **문자열로 변환**한다.

</aside>

## 4. HTML을 파싱하여 DOM Tree 생성

*`파싱`: 프로그래밍 언어의 문법에 맞게 작성된 텍스트 문서를 읽고 실행하기 위해 텍스트 문자의 문자열을 **분해**하고 **구조를 생성**하는 일련의 과정

<aside>
📌 **파싱을 하는 이유**

---

$\because$ 서버가 응답으로 보내주는 HTML 문서는 문자열로 이루어진 순수한 텍스트

$\therefore$ 브라우저가 이를 이해하기 위해서는 번역하는 과정 필요

</aside>

1. 문자열로 변환된 HTML 문서를 읽어 들여 문법적으로 더이상 나눌 수 없는 기본적인 언어 요소인 **토큰*token으*로 분해**한다.
2. 각 토큰을 객체로 변환하여 노드*node 생성*
    - 노드는 나중에 DOM을 구성하는 기본 요소가 됨
    - 노드의 중첩 관계에 의해 부자관계가 형성된다.
3. 부자 관계를 반영하여 모든 노드를  트리 자료구조로 구성
    
    ⇒ `DOM Document Object Model`; 브라우저가 이해할 수 있는, 노드들로 구성된 트리 자료구조
    

<aside>
➡️ **DOM = HTML 문서를 파싱(= 분해 & 구조 생성)한 자료구조 형태의 결과물**

</aside>

### 중간에 style 태그가 나오면 CSSOM Tree 생성

*`렌더링 엔진`: 내용 정보인 HTML, XML과 서식 정보인 CSS, XML 등을 읽어 들여 사람이 읽을 수 있는 문서로 표시하는 웹 브라우저의 핵심 기능을 담당하는 소프트웨어

렌더링 엔진은 처음부터 한 줄 씩 순차적으로 파싱하며 DOM 트리를 생성한다. 

이때, 중간에 CSS를 로드하는 **link나 style 태그를 만나면** DOM 생성을 **일시 중단**한다.

1. DOM 생성 일시 중단
2. CSS 파일 파싱
    - 파싱 과정은 HTML과 동일하다.
3. CSSOM*CSS Object Model* 생성
4. 파싱 완료 후, HTML 파싱이 중단된 시점으로 돌아가 다시 HTML 파싱

### 중간에 script 태그가 나오면 AST 생성 후 실행

<aside>
📌 **브라우저 렌더링이 반복되는 경우(`Rerendering`)**

---

1. 자바스크립트에 의한 노드 추가 또는 삭제
    
    ex.`Element.insertAdjacentHTML()`
    
2. 브라우저 창의 리사이징에 의한 뷰포트 크기 변경 
3. HTML 요소의 레이아웃에 변경을 발생시키는 스타일 변경
    
    ex. width, height
    

⇒ 리렌더링은 성능에 악영향을 준다. ($\because$ 파일을 다 다시 읽어야 함)

⇒ JS로 과하게 노드를 제어하거나 `display:none;`을 주었다가 다시 보여주기 남용 ❌

</aside>

1. DOM 생성 일시 중단
    
    <aside>
    📌 `**script` 태그의 위치와 블로킹**
    
    `<script src=””></script>`를 만나면 동기적으로 이루어지던 파싱이 중단된다.
    
    즉, `script` 태그 위치에 따라 DOM 생성이 지연될 수 있다.
    
    ---
    
    *`동기적*synchronous*`; 작업을 요청했을 때 그 작업이 종료될 때까지 기다린 후 다음 작업을 수행
    
    *`비동기적*asynchronous*`; 작업을 요청했을 때 그 작업이 종료될 때까지 기다리지 않고 다른 작업을 하고 있다가 요청했던 작업이 종료되면 그에 대한 추가 작업을 수행
    
    `body` 요소의 가장 아래에 `script` 태그를 위치하는 것이 상대적으로 더 **권장된다.**
    
    $\because$ DOM이 완성된 후 JS가 DOM 조작 → 엘리먼트를 찾지 못하는 오류 ❌
    
    $\because$ HTML 블로킹이 없어 페이지 로딩 시간 ⬇️
    
    <aside>
    📌 **`body` 맨 하단에 `script` 태그 작성은 필수?**
    
    ---
    
    - `body` 위에 위치한 경우
        
        ➡️ JS 파일 크기가 크고 인턴세 환경이 느리다면 페이지 보는 데에 오랜 시간 소요
        
    - `body` 아래에 위치한 경우
        
        ➡️ 페이지를 먼저 볼 수는 있음 but 페이지가 JS 파일에 의존적인 경우 불완전한 페이지
        
    
    → 상황에 맞는 다양한 경우를 고려해서 코드를 짜야함
    
    </aside>
    
    </aside>
    
2. script 태그 내 JS 코드 파싱
    1. 렌더링 엔진이 자바스크립트에게 제어권을 넘긴다. ; `blocking` 발생
    2. 소스코드를 토큰으로 분해
    3. 토큰으로 AST(추상 구문 트리) 생성
3. 바이트 코드로 변환 후 인터프리터 실행
    
    *`DOM api`: DOM이나 CSSOM을 변경하는 api
    
    <aside>
    📌 이때 DOM API가 사용될 경우, DOM과 CSSOM이 변경된다.
    
    변경된 DOM과 CSSOM은 다시 렌더 트리로 결합되며 리렌더링된다.
    
    → `reflow`; 레이아웃 계산을 다시 해주는 것
    
    → `repaint`; 재결합된 렌더 트리를 기반으로 다시 페인트 하는 것
    
    </aside>
    
4. HTML 파싱이 중단된 시점으로 돌아가 다시 HTML 파싱
    - JS 파싱과 실행 종료 후 제어권은 다시 렌더링 엔진으로 넘어감

## 5. DOM + CSSOM = Render Tree 생성

DOM과 CSSOM 생성이 완료되면 결합하여 Render 트리 생성.

- 렌더 트리는 화면에 보여지지 않는 것들을 포함하지 않는다.
    
    ex. HTML `meta` 태그, CSS의 `display:none;` 등
    
- 렌더 트리는 HTML 요소의 **레이아웃(위치, 크기)을 계산하는 데에 사용된다.**

<aside>
➡️ **렌더 트리는 브라우저 화면에 픽셀을 렌더링 하는 페인팅 처리에 입력된다.**

</aside>

# Operation

## 6. Render Tree에 있는 node를 배치(Layout)

## 7. Render Tree에 있는 node의 UI를 그림(Paint)

## 8. Render Tree에 있는 node를 순서대로 구성(Composition)

## 9. 웹 사용자에게 결과 화면을 출력

## 참고 자료

[[JavaScript]　브라우저 렌더링 과정(원리)](https://oliviakim.tistory.com/80)

[[192일차]nodejs환경과 브라우저 환경의 차이](https://sleepybird.tistory.com/153)

[[Node.js] 노드와 브라우저의 차이](https://velog.io/@shitaikoto/Node.js-browser)

[[번역] Browser에 www.google.com을 검색하면 어떤 일이 일어날까?](https://devjin-blog.com/what-happen-browser-search/)
