# API 명세서란?

- API 명세서란 `서버`개발자와 `클라이언트` 개발자가 약속을 하는 것이다. 예를들어, 어떤 URI에 A라는 요청을 하면 B라는 응답을 주겠다, A라는 요청에는 어떤 것이 필요하다 등등의 약속을 하는 것이다. 
- 클라이언트가 서버에서 만든 API를 사용하기 위한 설명서이다. 

<br>

# API 명세서 wiki로 만들기

![스크린샷 2020-11-17 오전 2 38 22](https://user-images.githubusercontent.com/45676906/99287797-09c7a000-287e-11eb-8783-a452bdcf729c.png)

먼저 Github 레포지토리에 들어오면 위와 같은 화면을 볼 수 있고, 여기서 `wiki` 버튼을 눌러보자. 

<img width="1792" alt="스크린샷 2020-11-17 오전 2 40 15" src="https://user-images.githubusercontent.com/45676906/99288008-590dd080-287e-11eb-93fb-b741cc0288f5.png">

그리고 `Create first page` 버튼을 누르고 쭉 다음을 눌러서 만들어보자.

<br>

![스크린샷 2020-11-17 오전 2 40 32](https://user-images.githubusercontent.com/45676906/99288175-8f4b5000-287e-11eb-9ae2-fb4fe3436c1e.png)

그러면 위와 같은 화면을 볼 수 있다. 여기서 `New page`를 눌러보자. 

![스크린샷 2020-11-17 오전 2 43 38](https://user-images.githubusercontent.com/45676906/99288367-d3d6eb80-287e-11eb-9197-193741beaa9a.png)

<br>

### API 명세서 내용

- `URI`는 무엇인가? (ex: /users/signup)
- `HTTP Method`를 어떤 것인가?(ex: GET, POST, PUT, DELETE)
- `Content-type` 명시하기 (ex: `Content-Type: application/json` => Reqeust-Body, Response-Body의 데이터 형식에 대해 적어주면 된다.(application-json은 json 형식으로 보내겠다는 뜻이다.)
- `Request Header`에는 어떤 것이 담기는가? (ex: AccessToken)
- `Request Body`에는 무엇이 오는지를 적어주면 된다. (ex: 회원가입이라면 loginId, password)
- 서버에서 응답으로 어떻게  `Response Body`가 만들어질 것인지?
- 클라이언트에서 필요한 데이터를 보내지 않았거나, 서버 에러가 발생하면 어떤 응답을 줄 것인지 적어주면 된다. (에러, 예외 처리)

<br>

<img width="1792" alt="스크린샷 2020-11-17 오전 2 45 57" src="https://user-images.githubusercontent.com/45676906/99288486-07197a80-287f-11eb-85cb-eef3601c0b10.png">

위에는 마크다운으로 작성할 수 했다는 것을 보여주는 것이다. 

![스크린샷 2020-11-17 오전 2 49 45](https://user-images.githubusercontent.com/45676906/99288877-932ba200-287f-11eb-8b5c-57c734996f6e.png)

<img width="1792" alt="스크린샷 2020-11-17 오전 2 50 43" src="https://user-images.githubusercontent.com/45676906/99288971-b1919d80-287f-11eb-91c3-7a338587c0af.png">

위와 같은 형태로 작성할 수 있고 자세히 보고 싶다면 [여기](https://github.com/wjdrbs96/Gyunny_Spring_Study/wiki/%5BPOST%5D-%EB%A1%9C%EA%B7%B8%EC%9D%B8) 에서 확인하면 된다.

<br>

## 정리

- API 명세서는 `notion`, `swagger`, `wiki` 등등 다양한 방법으로 작성할 수 있다. 
- 클라이언트와 약속이기 때문에 올바르게 적어야 서로 문제 없이 개발하며 소통할 수 있을 것이다.