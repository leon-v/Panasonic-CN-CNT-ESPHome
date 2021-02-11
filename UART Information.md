# CN-CNT Pinout
```
CN-CNT Pin-out (from top to bottom)
1 - +5V (250mA)
2 - 0-5V TX
3 - 0-5V RX
4 - +12V (250mA)
5 - GND
```

# Protocaol Info
As example 43 byte value to get DHW set temperature b1 (HEX) = 177(DEC) - 128 = 49 C ?
Mayeb they are just signed ints ?
Panasonic query, answer and commands are using 8-bit Checksum to verify serial data ( sum(all bytes) & 0xFF == 0 ). Last byte is checksum value. ?

# Protocol info packet ?:
To get information from heat pump, "magic" packet should be send to CN-CNT:

```
71 6c 01 10 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 12
```

## Protocol byte decrypt info ?:

Best reference for my heat pump is: https://github.com/hotswapster/panasonic-aircon-wifi

Soem very good reading about the protocol is: https://github.com/Egyras/HeishaMon