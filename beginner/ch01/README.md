> 이 포스트는 [널널한 개발자님 강의](https://www.inflearn.com/course/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%ED%95%B5%EC%8B%AC%EC%9D%B4%EB%A1%A0-%EA%B8%B0%EC%B4%88/dashboard)를 참조하여 작성한 포스트입니다.

## OSI 7 layer와 식별자

![](https://velog.velcdn.com/images/bini/post/9c739b72-c188-4dad-8b97-380d97624109/image.png)

L1계층(Physical)은 전선의 규격, 신호의 세기, 전압의 크기등 이런 물리적인 것들을 다루는데 여기서는 생략을 하도록 하자. L2계층(Data-Link)에서는 Ethernet(유선 네트워크)에 대해 알아 볼 예정이며 L3계층(Network)에서는 기본적으로 많이 있지만 그 중에서도 Internet에 대해서만 알아볼 것이다. 그리고 인터넷 프로토콜 기반으로 돌아가는 L4계층에서는 TCP, UDP에 대해 알아 볼 예정이며 L5에서는 SSL(TLS) L7에서는 HTTP 프로토콜에 대해 알아 볼 예정이다.

> L7의 HTTP와 L5의 SSL을 합쳐서 HTTPS라는 프로토콜이 나왔다.

이런식으로 OSI Layer를 분류했을 때 L1~L2는 NIC + Driver, L3는 IP, L4는 TCP, L5~L7은 Chrome App 같은것을 커버한다.

식별자란 우리의 주민번호, 이름등이 식별자이다. 식별자라는것은 어떤 대상을 식별하는 것인데 여기서 중요한 것이 식별자는 식별하는데에 대한 어떤 증거가 있는데 그게 중요하다.

L2수준에서 식별자는 MAC Address(H/W 주소)가 있는데 이 MAC 주소가 NIC를 식별한다. 즉, MAC주소는 주민등록번호가 사람한테 붙듯이 MAC주소도 NIC에 붙는다. 만약 NIC가 3개 붙은 PC가 있다고 하면 MAC주소도 3개가 될 것이다.

L3수준에서 식별자는 IP주소이다. IP주소에는 Version이 있는데 V4, V6라는 버전이 있다. 이 중에서도 V4 버전을 살펴볼 예정이다.

L4수준에서 식별자는 Port번호인데 Port번호는 관점에 따라 무엇을 식별하는지 달라진다. 만약 관점을 L2로 두면 Port번호는 인터페이스 식별자이다. 여기서 인터페이스란 LAN 케이블과 스위치의 연결 접점이라고 생각하면 좋다. 만약 과점을 L3~L4로 두면 웹 서비스 식별자라고 하며 L5~L7으로 보면 Process 식별자라고 한다.

내 PC의 연결된 ip주소, mac주소등을 알고 싶다면 터미널에 아래와 같이 작성하면 된다.

```shell
ifconfig
```

추가적으로 OSI 7 Layer 말고 DoD 4 Layer가 있는데 L1~L2는 Network Access 계층이라고 부르고 이것은 H/W 관점에서 설명하는 계층이고 L3계층은 똑같이 Internet 계층, L4계층을 Host to Host 계층, L5~L7은 Application 계층이라고 불린다.
