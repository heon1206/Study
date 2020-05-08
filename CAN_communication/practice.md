
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
![CAN_dataframe](https://github.com/heon1206/Study/blob/master/CAN_communication/img/CAN_data_frame.jpg)

