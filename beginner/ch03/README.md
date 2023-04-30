> 이 포스트는 [널널한 개발자님 강의](https://www.inflearn.com/course/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%ED%95%B5%EC%8B%AC%EC%9D%B4%EB%A1%A0-%EA%B8%B0%EC%B4%88/dashboard)를 참조하여 작성한 포스트입니다.

## IPv4주소의 기본 구조

OSI 7 Layer를 다시 생각해보면 L2에는 Ethernet, L3에는 IP, L4에는 TCP/UDP, L5는 SSL(TLS), L7은 HTTP로 대표적인 프로토콜이 존재한다. 여기서 MAC주소는 L2계층에서 가장 중요한 식별자이다. 그리고 48bit 주소체계를 가진다. 그리고 IPv4 환경의 IP주소는 32bit 주소체계를 가지는데 32bit는 8bit가 4개 모인것이다. 여기서 주목해야할 것은 8bit이다.

일단 IPv4환경의 IP주소는 32bit주소체계를 어떤 구성에 따라 쪼개서 관리한다. 그런데 8bit는 2^8=256가지로 0~255까지 나올수다.

> 💡 참고
> 255는 2진수로 1111 1111이고 이것은 앞서 애기한 broadcast로 여러가지를 고민해야한다.

> 💡 참고
> 192.168.x.x를 사설 IP주소라고 한다.

그럼 IP를 dot단위로 나눠보면 각각 8bit로 구성이된다. 즉 범위는 0~255까지 나올 수 있다.

![](https://velog.velcdn.com/images/bini/post/01440507-3825-4b04-81c0-4fa2cfda4f8f/image.png)

예로 192.168.0.10이라는 IP가 있다면 192.168.0과 10으로 나눌수 있는데 이렇게 나누는 것은 24bit와 8bit로 나누는 것인데 24bit쪽을 N/W ID, 8bit쪽을 Host ID라고 한다.

IP주소는 기본적으로 host에 대한 식별자이다. 즉, 인터넷 프로토콜을 쓰는 인터넷 망에서 인터넷에 연결된 컴퓨터 1대를 식별하기 위해 부여된 고유번호이다.

결국 IP주소는 N/W ID와 Host ID로 나눠진다. 우리나라 주소체계로 치면 서울시 강남구 삼성동 xx번지에서 서울시 강남구 삼성동이 N/W ID이고 xx번지가 Host ID이다.

예로 들어보자. 내가 택배를 시켰다고 가정해보자. 나는 서울시 강남구 삼서동 xx번지에 산다고 했을때 나한테 택배올려면 전국 택배물류 센터에서 우리 삼성동을 담당하는 물류센터로 먼저 배송이 되야하고 그 물류센터에서 택배차에 택배를 싣고 거기서 xx번지로 우리 집에 택배가 올 것이다. 즉 삼성동 물류센터가 N/W ID이고 xx번지에 해당되는 택배차가 Host ID이다.

## L3 IP Packet으로 외워라

- Packet이라는 말은 L3 IP Packet으로 외우자.
- Header와 Payload로 나뉘며 이는 상대적인 분류이다.
- 최대 크기는 MTU

Packet이라는 말은 네트워크 공부하면서 제일 많이 듣는 용어이다. Packet은 어떤 단위의 데이터이다. 쉽게 생각해서 레고의 블록조각을 의미한다. 번역하면 보쌈인데 쉽게 애기해서 뭔가 감싸서 하나의 단위 데이터로 만들었다는게 핵심이다.

위에서 Packet을 L3 IP Packet이라고 외우라고 했는데 이유가 Packet을 언급하면 연관검색어처럼 IP가 따라다닌다. 즉, Packet이라고 말을 하면 IP 프로토콜 환경이라고 생각하면 된다.

Packet은 논리적 구조로 보면 header와 그의 상대적인 개념으로 Payload로 나눠지는데 이 구조는 L2 Frame과 유사하다.

Packet의 최대 크기는 MTU라는 단위를 쓴느데 MTU 범위는 header 시작점부터 Payload끝까지를 의미하며 크기는 1500byte정도로 굉장히 작다. Packet을 예시로 택배박스라고 생각하면 좋을 것이다. 택배박스를 생각하면 송장이 있고 송장에는 출발지 목적지가 있고 택배박스 안에 택배 상품이 있는것처럼 Packet도 header라는 송장이 있고 내용물의 Payload가 존재한다.

> [WireShark](https://www.wireshark.org/)라는 프로그램으로 packet 정보를 확인이 가능한데 확인해보면 16진수 덩어리고 이루어진다. wireshark는 protocol decoder, Analyzer, sniffer로 불리며 의사로 치면 청진기로 packet을 수집 분석을 하고 장애시 원인분석을 할 수 있다.

## Encapsulation과 Decapsulation

### Encapsulation

- 별것 아니다. 러시아 전통 목각 인형인 마트료시카 인형을 떠올리자.

패킷을 애기하면 따라다니는게 Encapsulation이다. Encapsulation은 어떤 물건이 있으면 우리가 택배박스를 구해와 물건을 포장하고 택배박스에 넣고 테이핑을 한다. 이렇게 감싸가지고 안에 집어 넣는 행위를 Encapsulation이라고 한다. 여기서 '집어 넣는다'라는 행위에 대해 트징이 어떤 단위로 바꿨다, 단위화했다는 것이다. 그리고 이렇게 택배박스로 집어넣으면 택배기사님은 이게 어떤 물건인지 확인이 어렵다. 즉 단위화작업은 한편으로 남에게 못보게 캡슐화했다라고 볼 수 있다. 이걸 N/W 버전으로 보면 아래와 같다.

### En/Decapsulation

![](https://velog.velcdn.com/images/bini/post/d279feef-8176-4312-a56d-d319a490d775/image.png)

실제 네트워크 버전으로는 L2 Frame안에 payload에 L3 Packet이 들어가고 Packet Payload 안에 L4 Segmant가 들어간다. 이렇게 집어 넣는게 Encapsulation 꺼내는 행위가 Decapsulation이다.
