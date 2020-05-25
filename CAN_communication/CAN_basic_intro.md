### CAN 개요
#### controller Area Network(CAN) 개념 및 등장 배경
* 차량 내에서 호스트 컴퓨터 없이 MCU나 장치들이 서로 통신하기 위해 설계된 통신 규격.
* 1985년 독일 Bosch사에 의해 개발, 1986년 사양이 공개되었으며, 1994년 ISO11898국제규격 등록으로 등록 됨.
* 차량 내 전자장치ECU가 증가 함에 따라ECU간 point-to-point방식의 통신은 배선장치 증가에 따른 비용, 복잡성, 무게 증가 등의 문제를 나타냄.
* CAN은 Multiple Master 구조로 여러 ECU가 하나의 Bus를 공유하여 통신하므로 배선을 줄일 수 있음(Bus Topology)
#### CAN  특징
* Bus topology를 가지는 Multiple Master 통신.
* 이론상 2032개의 Node를 하나의 Bus에 연결 가능
* Node 추가 및 재구성 가능
* 고속 통신(125kbps ~ 1Mbps)
* Twisted Pair 2선을 사용하여 전기적 노이즈에 강함
* Message Addressing
* 높은 신뢰성 및 오류 처리 기능
* 물리적 결함 추정 node의 버스 연결 차단
 <img src="https://user-images.githubusercontent.com/24906011/82777560-6f1b7500-9e89-11ea-8234-452ecfb2faf8.JPG" width = "50%">
#### CAN FD
* 2011년 CAN FD개발, 2012년 공개(ISO 11898-7)
* Flexible Data-rate: Arbitration phase와 Data phase에서의 전송속도가 다름
* 최대 12Mbps, Data field 0~64 - Bytes
* Control field, CRC field 내용 변경
* CRC field bit stuffing 내용 변경
#### CAN 규격
* 식별자(ID)의 길이에 따른 2가지 구분
-표준 CAN(버전 2.0A): 11비트 Message ID
-확장 CAN(버전 2.0B): 29비트 Message ID
-CAN 2.0A는 2.0B의 메세지 수신 불가

* ISO 규격에 따른 2가지 구분
-ISO11898: 128kbps~ 1Mbps 통신 가능(High-speed CAN)//반사파에 의한 노이즈 제거를 위해 종단저항이 필요
-ISO11519: 125kbps까지 통신 가능(Low-Speed CAN)//각 노드마다 종단저항 존재
<center><img src = "https://user-images.githubusercontent.com/24906011/82777558-6e82de80-9e89-11ea-9c7a-bc3828cca4af.JPG" width = 70%></center>

#### CAN Bus Logic
* CAN신호는 Dominant(Low, 0)과 Recessive(High, 1) Level로 구분됨.
* CAN Bus는 각 Node들의 출력 신호에 따라 Wired-AND로 구성되어 있으며 Dominant 신호를 출력하는 Node가 존재할 경우, Bus는 Dominant상태가 됨.
* 각 Node들은 출력과 동시에 Bus의 상태를 확인하며, 이에 따라 Arbitration, Error Check등이 이루어짐.
* 한 노드라도0이면 버스가 0
<center><img src = "https://user-images.githubusercontent.com/24906011/82777556-6dea4800-9e89-11ea-81d1-fc3761b64bf4.JPG" width = "50%"></center>

#### Signal Encoding and Bit Stuffinng
* NRZ(Non Return-to-Zero) Encoding
-NRZ는 Logical bit level을 물리적으로 표현할 때 매번 0V로 신호를 변환하지 않는 것을 의미함.
-1bit time 당 1 sampling으로 충분.(장점)
-연속적인 동일 bit lebel에 대해 오차 누적 가능성이 존재함.
-이를 해결하기 위해 Bit Stuffing이 이루어짐.

<center><img src ="https://user-images.githubusercontent.com/24906011/82777562-6fb40b80-9e89-11ea-9d39-4c7729a98cef.JPG"> </center>

- Bit Stuffing
-5회의 동일 Bit연속 전송 시 반전된 1 Stuff Bit를 삽입.
-수신 단에서는 Stuff Bit을 빼고 수신하여 메시지 복원


