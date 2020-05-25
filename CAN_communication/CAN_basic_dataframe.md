
### CAN 개요
- #### CAN이란?
CAN 등장 배경과 특징
Network Topologt
- ####  CAN 규격
Standard /Extended
High-Speed/ Low-speed
- #### CAN Bus Logic
Dominant/ Recessive/ Wired-And
NRZ Encoding
Bit Stuffing
### CAN Protocol 1
- #### CAN Message Frame
Data Frame
### CAN Protocol 2
- #### CAN Message Frame
- Remote Frame
- Overload Frame
- Error Frame
- CAN Error Handling


---

### Messge Frame Types
- Data Frame
 TransMitter가 하나 또는 다수의 Receiver에게 전송하는 데이터가 담긴 Message Frame.

- Remote Frame
 특정 ID의 Data Frame Message 전송을 요구하는 Message Frame.
 - Overload Frame
 Data / Remote Frame 사이의 시간 지연을 위해 사용되는 Message Frame.
 - Error Frame
 오류가 발생했음을 알려주는 Message Frame.
---
### Data Frame
![CAN_dataframe](https://user-images.githubusercontent.com/24906011/81359534-5c2c4500-9114-11ea-8487-fe02c4b5c241.jpg)
####   Arbitration Field(standard - 12bits, extended - 32bits)
- **SOF(1-bit, 0)**: Start of Frame, Frame의 시작을 의미
- **RTR(1bit)** : Data Frame(0) or Remote Frame(1) -> SRR(1)//데이터, 리모트 판단
- **IDE(1bit)**: standard(0) or extended(1) fromat//이후의 비트들이 어떤 field일지 판단
####  Data Frame -ID Field & priority

![CAN_bus_arbitration](https://user-images.githubusercontent.com/24906011/81371265-5f362e00-9132-11ea-839c-e78146b720dd.jpg)
- Identifier field(11bits) 를 기준으로 그 Message ID값이 작을 수록 높은 우선순위를 가짐.
- RTR bit(1bit) 또한 Arbitration에 영향을 주며, 이는 Data Frame과 Remote Frame중 Data  Frame에 우선권을 부여
#### Data Frame - Control Field(6bits)
- **IDE /r1 (1bit)**: standard(0) or extended(1) format
- **r0 (1bit, 0)**: Reserved
- **DLC(4bits)**: Data Length Code, Data Field 크기 결정(최대 8-Bytes)
(CAN FD: 최대 64-Bytes)

#### Data Frame - CRC Field(Cyclic Redundancy Check Field, 16bits)
- **CRC Sequence(15bit)**: CRC Field 이전의 모든 bit의 이상 유무 확인용 코드. 
SOF, Arbitration field, Control Field, Data Field + 15bits
X^15^+X^14^ +X^10^ +X^7^ +X^4^ +X^3^+1(generator - polynomial)
=> CRC Sequence
- **CRC Delimiter(1bit,1)**: Reserved
#### Data Frame - ACK Field(Acknowledge Field, 2bits)
- **ACK slot(1bit)**: Sender 는 1로 출력. 하나 이상의 Receiver가 정상적으로 Message를 수신했다면 0으로 출력하게 되고 Bus는  0(Dominant)가 되며, 이에 따라 Sender는 정상적인 통신이 이루어졌다고 판단. 만약 정상적으로 수신한 Receiver가 존재하지 않으면 1이 되며, Sender는 재송신을 시도.(ACK Error)
-  **ACK Delimiter(1bit, 1)**: Reserve
#### Data Frame - EOF(End of Frame, 7bits, 1)
- **EOF(7bits,1)**: Frame의 끝을 표시, 1로 고정(Bit Stuff 대상이 아님)
### IFS(Inter Frame Space, at least 3bits)
- **IFS**: Data Frame혹은 Remote Frame사이에 존재하여 이전 Frame과 분리하는 역할로 최소 3bits의 Recessive(1)bits로 구성.
- **Intermission(1,3bits)**: Intermission 동안에는 어떤 Node도 Data Frame이나 Remote Frame을 시작할 수 없고 Overload Frame만 가능
- **Suspended Transmission**: Error Passive Node의 Message 송신 후, 해당 Node는 8bits의 Recessive(1) bits를 Intermission(3bits)이후에 출력.
- **Bus Idle**: Bus Idle의 상태는 임의의 길이만큼 지속될 수 있으며, 어떤 Message의 통신도 이루어지지 않고 있는 상태로 Dominant(0)이 감지되면 새 Message Frame의 SOF로 간주.
### Data Frame
![CAN_data_frame_bit_explaination](https://user-images.githubusercontent.com/24906011/81371124-f18a0200-9131-11ea-88ae-666c68f31627.JPG)
