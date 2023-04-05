# ESP-CSI

The main purpose of this project is to extract AP beacon packet Channel state information(CSI) with ESP32 in sniffer mode. ESP driver has support to calculate Wi-Fi packet CSI and you can access or analysis original CSI data.

## Supported versions and ESP32 target

| ESP-CSI | Dependent ESP-IDF |        support Target       |
| :-----: | :---------------: | :-------------------------: |
|  main   |   release/v5.0    | ESP32 / ESP32-S2 / ESP32-C3 |

## ESP-Sniffer-mode
ESP sniffer mode can monitor packet that are transmitting in current channel. Even the packet mac destinantion is not as same as ESP mac address, the ESP can still receive the packet instead of fillter it. In addtion, the ESP sniffer mode has fillter function, which means that the application can decided which specific type of packet can be received.

The fillowing types of packets can be capture by ESP:
  - 802.11 Management frame Type(0x00)
  - 802.11 Control frame Type(0x01)
  - 802.11 Data frame Type(0x02)

The above three types are most mojority types of 802.11 frame. You could choose to fillter one or more types that you need to receive by ESP.

## beacon frame specifiction
Beacon frame is a subtype of 802.11 management fram with subtype(0x80). Beacon is a periodicity frame and sent by AP in every certain interval to announce that AP is exist and wait for connect. In addtion, beacon frame is a boradcast frame with destination address(FF:FF:FF:FF:FF:FF).

## CSI Data Format
type,seq,mac,dmac,rssi,rate,sig_mode,mcs,bandwidth,aggregation,stbc,fec_coding,sgi,noise_floor,ampdu_cnt,channel,secondary_channel,local_timestamp,ant,sig_len,rx_state,len,first_word,data
CSI_DATA,0,1c:b9:c4:b5:a9:58,ff:ff:ff:ff:ff:ff,-67,10,0,0,0,0,0,0,0,-96,0,1,0,62577,0,220,0,128,1, [-36,-64,13,0,0,9,6,8,11,6,18,6,24,4,33,4,33,5,37,4,35,7,33,4,34,1,30,0,25,1,17,-3,9,-6,2,-15,-8,-19,-11,-23,-16,-30,-16,-34,-16,-40,-16,-44,-12,-44,-8,-37,-2,-35,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,-6,-1,-5,-4,-3,-7,1,-10,2,-12,6,-9,7,-9,10,-9,11,-10,10,-7,10,-5,11,-5,6,-5,3,-3,0,-3,-3,1,-7,5,-10,6,-12,9,-18,11,-20,12,-24,13,-22,10,-22,9,-23,7,-18,8]
CSI_DATA,1,1c:b9:c4:b5:a9:58,ff:ff:ff:ff:ff:ff,-67,10,0,0,0,0,0,0,0,-96,0,1,0,164996,0,220,0,128,1, [-36,-64,13,0,-3,8,1,11,9,15,11,16,18,20,25,21,23,24,27,27,25,25,26,25,23,18,25,16,20,12,15,6,14,0,10,-8,4,-19,5,-26,6,-33,8,-37,10,-40,15,-42,18,-39,19,-32,20,-26,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,-7,-1,-5,-2,-2,-6,4,-7,6,-8,6,-6,9,-6,12,-5,13,-3,11,-3,12,2,9,0,7,0,1,-1,0,-1,-5,-1,-8,0,-11,1,-17,0,-19,1,-24,0,-27,-1,-25,-2,-25,-4,-22,-3,-19,0]
CSI_DATA,2,1c:b9:c4:b5:a9:58,ff:ff:ff:ff:ff:ff,-67,10,0,0,0,0,0,0,0,-96,0,1,0,371414,0,220,0,128,1, [-36,-64,13,0,-8,1,-4,6,-3,13,-3,20,0,23,3,29,3,34,4,36,3,33,8,32,8,29,6,27,7,22,6,14,7,6,7,-3,9,-12,12,-19,14,-25,17,-30,21,-32,23,-33,25,-30,26,-25,24,-21,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,-8,3,-5,8,-1,6,3,6,4,7,6,6,11,5,12,4,13,2,12,1,12,-1,9,-2,8,0,2,-3,-2,-4,-4,-6,-6,-7,-12,-10,-13,-10,-19,-10,-21,-7,-22,-9,-20,-9,-22,-6,-20,-7,-16]
CSI_DATA,3,1c:b9:c4:b5:a9:58,ff:ff:ff:ff:ff:ff,-67,10,0,0,0,0,0,0,0,-96,0,1,0,574595,0,220,0,128,1, [-36,-64,13,0,5,1,6,0,10,-12,13,-15,15,-20,17,-26,20,-28,19,-31,19,-31,17,-32,13,-30,10,-25,7,-22,1,-16,-2,-9,-10,-3,-16,4,-24,5,-32,8,-37,7,-40,7,-38,6,-42,4,-34,-1,-33,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,-5,4,-7,-1,-6,-4,-8,-9,-4,-11,-4,-13,-2,-15,-1,-16,2,-17,4,-15,3,-13,5,-9,4,-6,4,-3,1,2,1,8,-1,8,-3,15,-3,17,-4,20,-4,24,-6,24,-8,22,-8,23,-6,22,-3,17]
CSI_DATA,4,1c:b9:c4:b5:a9:58,ff:ff:ff:ff:ff:ff,-66,10,0,0,0,0,0,0,0,-96,0,1,0,678025,0,220,0,128,1, [-36,-64,13,0,1,0,7,-3,10,-13,13,-17,13,-22,15,-30,16,-30,15,-37,17,-38,12,-40,6,-31,10,-26,6,-24,3,-19,-2,-11,-8,-2,-15,2,-23,8,-29,13,-33,16,-38,13,-40,11,-37,5,-35,9,-27,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,-7,2,-7,-3,-8,-6,-7,-10,-4,-13,-4,-13,-2,-13,-1,-14,2,-17,2,-14,3,-11,5,-9,4,-6,3,-2,2,3,2,7,0,11,1,16,0,19,0,23,-3,25,-3,27,-2,25,-3,26,-4,23,-1,19]

|  Type    | Name               | Description
|  --------| ----               | ------------
|          | CSI_DATA           | Data type is CSI
|  uint32  | seq                | Received data sequence
|  uint8   | mac                | Source MAC address
|  uint8   | dmac               | Destination MAC address
|  int     | rssi               | Received Signal Strength Indicator of packet with unit: dBm
|  uint    | rate               | PHY rate. Only valid for non HT(11bg) packet
|  uint    | sig_mode           | 0: non HT(11bg) packet; 1: HT(11n) packet; 3: VHT(11ac) packet
|  uint    | mcs                | Modulation Coding Scheme
|  uint    | bandwidth          | Channel Bandwidth. 0: 20MHz; 1: 40MHz;
|  uint    | aggregation        | 0: MPDU packet; 1: AMPDU packet
|  uint    | stbc               | Space Time Block Code. 0: non STBC packet; 1: STBC packet
|  uint    | fec_coding         | Flag is set for 11n packets which are LDPC
|  uint    | sgi                | Short Guide Interval. 0: Long GI; 1: Short GI
|  uint    | noise_floor        | Noise floor of Radio Frequency Module. unit: dBm
|  uint    | ampdu_cnt          | Ampdu cnt
|  uint    | secondary_channel  | Secondary channel. 0: none; 1: above; 2: below;
|  uint    | timestamp          | The local time when this packet is received. unit: microsecond
|  uint    | ant                | Antenna number that receive packet, 0 and 1
|  uint    | sig_len            | Length of packet
|  uint    | rx_state           | State of the packet. 0: no error; others: it contain error
|  uint16  | len                | Length of csi data
|  bool    | first_word         | Flag of first four bytes of the CSI Data. 0: vaild; 1: invaild
|  int8    | data               | Buffer of CSI Data. The data are interleaved and first one is imaginary part, second one is real part.

## Get Beacon CSI From AP

<img src="img/get_ap_CSI.png" width="400">

The multiple APs will continuously send out beacon frame in specific channel to announce their exist. The ESP which is running the sniffer mode will monitor management frames and receive beacon frames to calculate CSI. It can receive multiple beacon frames from different APs as long as beacon frams is sent out in specific channel that ESP is currently waitting. 