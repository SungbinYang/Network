> 이 포스트는 [널널한 개발자님 강의](https://www.inflearn.com/course/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%ED%95%B5%EC%8B%AC%EC%9D%B4%EB%A1%A0-%EC%9D%91%EC%9A%A9/dashboard)를 참조하며 작성하였습니다.

## 세 가지 네트워크 장치 구조

- Inline: Packet + Drop/Bypass + Filtering
- Out of Path: Packet + Read Only, Sensor
- Proxy: Socket Stream + Filtering

3가지 네트워크 장치 구조로 Inline, Out of Path, proxy가 있다. 근데 Inline하고 Out of Path의 특징이 있는데 둘다 패킷을 다룬다는 점이다. proxy는 socket stream 데이터를 다룬다. 즉 데이터를 무슨 데이터를 다루냐에 따라 장치구조가 바뀐다. 우리가 네트워크에 대해 공부를 할 때 보통은 네트워크를 이루는 스위치에 대해 배우는데 만약 처음 보는 네트워크 장치를 공부할 경우 제일 먼저 따질께 위의 3가지 구조중에 어떤 구조로 되어있는지 확인해봐야 한다.

Inline은 구조적으로 필터링이 된다. 공기청정기 필터처럼 생겼다. 공기가 필터를 거쳐나가는 것처럼 패킷이라는 데이터 단위가 Inline device를 통과해서 지나간다. 그런데 패킷이 통과하려 할 때 Bypass(통과)시킬지 혹은 Drop(차단)시킬지 정한다. 물론 Bypass를 한다해도 NIC가 여러개라고 하면 어느 인터페이스로 가야할 지 선택도 해야 한다. 이런 역할을 할때 Inline device를 설명하는 대표적인 장치가 Router이다.

Out of Path는 Inline처럼 패킷단위 데이터를 보내는 것은 같지만 Out of Path는 읽기만 한다. 즉, 무언가를 허용, 차딘이 없고 보기만 한다는 것이다. 그래서 Out of path는 무언가를 인지하는게 주된 목적이다. 그래서 만약에 네트워크 보안상 이슈를 인지하겠다고 하면 보안센서인거고 네트워크 장애를 인지하겠다면 장애 대응 센서가 되는 것이다. 그래서 ~ 네트워크 센서라고 한다면 거의 대부분 Out of Path 구조를 가지고 있다. 추가적으로 애기해보면 Tab 스위치라고 있는데 Tab 스위치라는 것을 통해서 패킷을 복사받는데 그 복사된 패킷을 읽고 분석해서 이게 어떤 현상인지를 결과를 알려주는게 일반적이다. 이런 장치들을 연결할 수 있는 포인트, 네트워크에서는 Tapping Point라고 하는데 그런 애들이 Tapping point에 연결되는 것들이 Out of Path 구조를 갖는다.

Proxy는 다루는 데이터 단위가 위의 2가지 구조와 다르다. Proxy는 네트워크 소켓 수준에서 무언갈 하다 보니 stream 데이터를 볼 수 있다는 장점이 있다. 패킷에서 스트림 데이터를 확인할려면 decapsulation해야하고 과정이 굉장히 복잡하다. 예로 10MB짜리 stream 데이터를 확인하려면 패킷 10,000개를 조립해야 한다. 즉, 패킷으로 확인해야 할께 있고 스트림 수준의 데이터로 확인해야할께 있는데 주로 파일수준의 user mode application단의 단위를 다루면 그때는 proxy 구조를 쓸 수 밖에 없다. proxy는 inline과 구성면에서 비슷한 면이 있다. 필터링이 가능하다는 면이고 read only 개념은 없다. proxy는 말 그대로 대리를 하는데 그래서 이 대리자를 통해서 무언갈 지나가기 때문이 이 proxy 입장에서는 application stream 전체를 다 모니터링 할 수 있다는 특징이 있다. 그래서 일단은 필터링이라는 개념에서는 인라인과 유사성을 같지만 다루는 데이터가 다르다.

패킷이라는 것을 논할려면 IP 스택 수준에서 논한다. proxy라고 하는 놈은 user-mode 영역에서 다루고 다루는 데이터의 단위는 stream일 것이고 OSI 7 Layer의 L5~L7을 커버한다. 예로 HTTP 프로토콜을 분석하려면 proxy가 유리하다. 그럼 L3에서 HTTP 프로토콜 분석이 불가능할까? 아까도 언급했지만 불가능하지는 않지만 매우 복잡하다.
