## **WebSocket이란** 

Transport protocol의 일종으로 쉽게 이야기하면 웹버전의 TCP 또는 Socket이라고 이해하면 된다.

WebSocket은 서버와 클라이언트 간에 Socket Connection을 유지해서 언제든 양방향 통신 또는 데이터 전송이 가능하도록 하는 기술이다.

Real-time web application구현을 위해 널리 사용되어지고 있다. (SNS어플리케이션, LoL같은 멀티플레이어 게임, 구글 Doc, 증권거래, 화상채팅 등)



**사용이유**

> 웹어플리케이션에서 기존의 서버와 클라이언트 간의 통신은 대부분 HTTP를 통해 이루어 졌으며 HTTP는 Request/response기반의 Stateless protocol이다.
>
> 즉, 서버와 클라이언트 간의 Socket connection같은 영구적인 연결이 되어있지 않고 클라이언트 쪽에서 필요할때 Request를 할때만 서버가 Response를 하는 방식으로 통신이 진행되는 한방향 통신이다. 이럴경우 서버쪽 데이터가 업데이트 되더라도 클라이언트 쪽에는 화면은 Refresh하지 않는한 변경된 데이터가 업데이트 되지 않는 문제가 발생한다. 이런 문제는 일반적은 웹어플리케이션에서는 기존의 있던 임시방편인 Long polling이라던가 Ajax를 사용해도 어느정도 해결이 가능하지만 데이터의 빠른 업데이트가 아주 중요한 요소 중에 하나인 어플리케이션에서는 실시간 업데이트가 아주 중요하기 때문에 Web Socket이 아주 중요한 기술로 사용되고 있다.
>
> Web Socket은 Stateful protocol이기 때문에 클라이언트와 한 번 연결이 되면 계속 같은 라인을 사용해서 통신하기 때문에 HTTP 사용시 필요없이 발생되는 HTTP와 TCP연결 트래픽을 피할 수 있다. 마지막으로 Web Socket은 HTTP와 같은 포트(80)을 사용하기에 기업용 어플리케이션에 적용할 때 방화벽은 재설정 하지 않아도 되는 장점이 있다.



**작동원리**

>서버와 클라이언트 간의 WebSocket연결은 HTTP프로토콜을 통해 이루어집니다. 만약 연결이 정상적으로 이루어 진다면 서버와 클라이언트 간에 WebSocket연결이 이루어지고 일정 시간이 지나면 HTTP연결은 자동으로 끊어집니다.



**HTTP통신방법과 WebSocket의 차이점**

> 결정적인 차이는 프로토콜이다.
>
> WebSocket 프로토콜은 접속 확립에 HTTP를 사용하지만, 그 후 통신은 WebSocket 독자의 프로토콜로 이루어진다.
>
> 또한, header가 상당히 작아 overhead가 적은 특징이 있다. 장시간 접속을 전제로 하기 때문에, 접속한 상태라면 클라이언트나 서버로부터 데이터 송신이 가능하다. 더불어 데이터의 송신과 수신에 각각 커넥션을 맺을 필요가 없어 하나의 커넥션으로 데이터를 송수신 할 수 있다. 





## WebSocket 객체 생성하기

- 속성  : https://developer.mozilla.org/en-US/docs/Web/API/WebSocket

- 예제 : https://developer.mozilla.org/ko/docs/WebSockets/Writing_WebSocket_client_applications

  

WebSocket 프로토콜을 사용하여 통신하기 위해서는 `WebSocket`객체를 생성해야 합니다. 이 객체는 자동으로 서버로의 연결을 열려고 할 것입니다.

WebSocket 생성자는 하나의 필수 파라미터와 하나의 선택 파라미터를 받습니다.

```html
WebSocket WebSocket(
  in DOMString url,
  in optional DOMString protocols
);
```

- `url`

  연결할 URL으로, 이것은 WebSocket 서버가 응답할 URL이어야 합니다.

- `protocols` Optional

  하나의 프로토콜 문자열, 또는 프로토콜 문자열의 배열입니다. 이 문자열들은 서브 프로토콜을 지정하는데 사용되어, 하나의 서버가 여러 개의 WebSocket 서브 프로토콜을 구현할 수 있도록 해줍니다. 예를 들어, 하나의 서버가 처리하는 상호작용이 지정된 `protocols`에 따라 달라지도록 할 수 있습니다. 만약 프로토콜 문자열을 지정하지 않으면 빈 문자열을 넣은 것으로 간주됩니다.

생성자는 예외를 발생시킬 수 있습니다:

- `SECURITY_ERR`

  접속을 시도하고 있는 포트가 차단되었습니다.