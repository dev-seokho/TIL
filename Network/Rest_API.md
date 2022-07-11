![](https://velog.velcdn.com/images/seo_kk/post/e24d6047-d731-4999-90d5-1264755033e6/image.png)

여러 IT회사에서 REST API는 면접 단골 질문이며, 현업에서도 많이 쓰이는 개념입니다.
저 또한 개발자로써 생활하며 REST API라는 단어를 많이 사용했었습니다.
실제로 이전 회사에서 쓰이는 API들이 RESTful하지 못하다고 생각해서, REST하게 바꿔 본 경험이 있습니다.
하지만 `왜 REST API를 사용해야하는가?`, `REST API란 무엇인가?` 라는 동료들의 물음에는 완벽하게 답변하지 못했었습니다.
그래서 이 글을 통하여 REST API란 무엇인지, 그리고 그 당시 회사에서 REST하게 개선했다고 생각한 API들이 정말 REST하게 개선됐었던 것인지 확인해보려고 합니다.

## REST란 
REST는 **RE**presentational **S**tate **T**ransfer(자원의 표현에 의한 상태전달)의 약자입니다.
REST는 2000년도에 로이 필딩(Roy Fielding)의 박사학위 논문에서 최초로 공개되었습니다.
로이 필딩은 HTTP의 저자 중 한 사람인데, HTTP 설계의 우수성에 비해서 제대로 사용하지 못하는 모습에 REST 아키텍처를 개발하게 됐습니다.
로이 필딩이 REST를 개발할 당시 WEB은 이미 빠른 발전을 이룬 상태였고, REST로 인해 WEB이 망가지지 않도록 독립적으로 만드는 것에 힘을 쏟았다고 합니다.
이러한 노력들이 REST 안에 잘 녹아들어가 있습니다.

🙆🏻‍♂️ REST는 자원을 정의하고 자원에 대한 주소를 지정하는 방법의 전반을 일컫는 아키텍처 중 하나이며, **REST의 정의**는 로이 필딩의 논문에서 다음과 같이 명시되어 있습니다.

> REST : **분산 하이퍼미디어 시스템(ex:web)을 위한 아키텍쳐 스타일**

웹같은 분산 하이퍼미디어 시스템을 위한 **제약조건의 집합**이라는건데, 이는 다음과 같습니다.

## REST를 구성하는 스타일(제약조건들)
#### 1. Client-Server
**✅ Server와 Client의 역할을 확실하게 하여 의존성 줄이기**
  
> Server는 API 제공, Client는 세션, 로그인 정보등 Client단에서 관리할 수 있는 것들을 관리합니다.
각각의 역할이 확실하게 구분되기 때문에, Server와 Client에서 개발할 내용이 명확해집니다.
또한 이는 서로간의 의존성을 줄여주는 이점을 줍니다.

#### 2. Stateless (무상태성)
**✅ 상태정보를 저장하지 않음으로서 구현을 단순화시키기**

> 상태정보를 저장하거나 관리하지 않습니다.
세션 정보나 쿠키 정보를 별도로 저장하거나 관리하지 않기 때문에 서버는 단순하게 들어오는 요청만 처리하면 됩니다.
이로 인해 애플리케이션의 자유도가 높아지고, 서버에서 불필요한 정보를 관리하지 않음으로 구현이 단순해집니다.

#### 3. Cache (캐시)
**✅ 캐싱 기능이 가능한 REST**
> HTTP 웹표준을 그대로 사용하기 때문에 웹의 인프라를 그대로 사용 가능하며, Client-Server 간에 캐싱 기능 적용이 가능합니다.
HTTP 표준에서 사용하는 Last-Modified태그, E-Tag를 이용하면 캐싱 구현이 가능합니다.

#### 4. Uniform Interface
**✅ HTTP 표준을 따르는 환경이라면, 언어와 플랫폼에 상관없이 사용할 수 있는 인터페이스 스타일**
>URI를 사용해서 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일(제약조건의 집합)을 말합니다.
Uniform Interface의 제약 조건은 4가지가 있습니다.
>>1. Identification of resources  
❗️리소스가 URI로 식별된다.
2. Manipulation of resources through representations
❗️리소스를 CRUD할 때 HTTP에 표현을 담아야 한다.(GET, POST, PUT, DELETE)
3. Self-descriptive messages 
❗️메세지는 스스로를 설명할 수 있어야 한다.
4. Hypermedia as the engine of application state (HATEOAS)
❗️애플리케이션의 상태는 항상 Hyperlink를 이용해 전이되어야 한다.

#### 5. Layered System
**✅ 다중 계층 구성을 지원하여 중간 매체 사용이 가능하게 하기**

> REST 서버는 다중 계층으로 구성될 수 있으며, 보안, 로드밸런싱, 암호화 계층을 추가하여 구조상 유연성을 가질 수 있습니다.
또한 Proxy, Gateway 같은 네트워크 기반의 중간 매체를 사용할 수 있게 합니다.

#### 6. Code-On-Demand(optional)
**✅ feat. JS**
>
요청을 받으면 Server에서 Client로 실행 가능한 코드를 전송하여 클라이언트의 기능을 확장할 수 있는 기능입니다. (JavaScript)

## REST의 구성 요소
#### 1. 자원(Resource) : URI
> 모든 자원은 URL를 가지고 Client는 자원의 상태를 조작하기 위해 URL로 요청을 보냅니다.

#### 2. 행위(Verb) : HTTP Method
> Client는 URI를 이용해 자원을 조작하기 위해 HTTP Method(GET, POST, PUT, DELETE 등)를 사용합니다.

#### 3. 표현(Representations)
> Client가 Server로 Request를 보냈을 때 서버가 Response로 보내주는 자원의 상태를 Representations라고 합니다.
REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타낼 수 있습니다.

## REST API
앞에서 설명한 REST의 구성하는 스타일과 구성요소를 기반으로 서비스 API를 구현한 것을 REST API라고 할 수 있습니다.
그렇기 때문에 각 요청이 어떤 동작이나 정보를 위한 것인지 그 요청의 모습 자체로 추론할 수 있어야 합니다. **(Uniform Interface)**
OpenAPI를 제공하는 기업의 대부분은 REST API를 제공합니다.

## REST API 설계
🙆🏻‍♂️ REST API를 설계하는 방법은 다음과 같습니다.
#### 1. URI는 정보의 자원을 표현해야 합니다.
#### 2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현해야하며 URI에 포함되어서는 안됩니다.

#### 3. URI 는 명사를 사용해야합니다. (리소스명은 동사가 아닌 명사를 사용해야합니다.)
>❌  동사가 URI에 포함되어 있습니다.
[GET] http://localhost:8080/getUsers
⭕️  동사를 URI에 포함되어 있지 않습니다.
[GET] http://localhost:8080/users

#### 4. 슬래시 `/` 를 활용해서 계층관계를 표현합니다.
>⭕️ 슬래시를 통해 계층 관계가 나눠져 있습니다.
[GET] http://localhost:8080/users/3

#### 5. 밑줄 `_` 을 사용하지 않고 하이픈 `-` 을 사용합니다.
>❌ 밑줄을 사용하여 URI를 구성합니다.
[GET] http://localhost:8080/blogs/this_is_example
⭕️ 하이픈을 사용하여 URI를 구성합니다.
[GET] http://localhost:8080/blogs/this-is-example3

#### 6. URI는 소문자로만 구성합니다.
>

#### 7. Client는 해당 request에 대한 성공, 실패, 오류 등에 대한 피드백을 HTTP 상태 코드로써 받을 수 있도록 HTTP 응답 상태 코드를 사용해야합니다.
>

#### 8. 파일확장자는 URI에 포함하지 않습니다.
>❌ 확장자 `.jpg` 가 URI에 포함돼 있습니다.
http://localhost:8080/photo.jpg

#### 9. URI의 마지막은 슬래시를 포함하지 않습니다.
>❌ BAD [GET] http://localhost:8080/blogs/this_is_example
