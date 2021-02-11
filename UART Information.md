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
0x70 0x0a 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x86
```

# Protocol byte decrypt info ?:

Best reference for my heat pump is: https://github.com/hotswapster/panasonic-aircon-wifi

Soem very good reading about the protocol is: https://github.com/Egyras/HeishaMon

# Test log:

## 12-02-2021
Connected USB to UART to pins.
Noticed 5V on RX on the CN-CNT port. None the less, my adapter could drive it low(ish) to about 600mV.
I used the baud rate of 9600 since that is what i saw in HeishaMon [here](https://github.com/Egyras/HeishaMon/blob/697f6bd188d022d86f5908e06a0ea74835cda384/HeishaMon/HeishaMon.ino#L386).

Upon power up of the heat pump (by switcing the power supply to it off then on again) i recieved:
```
0x42 0x00 0x00 0x00 0x00 0x00 0x00 0x00
```

After the next power up, i recieved:
```
0x30 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00
```

I would expect something more consistient, i am questioning the baud rate of this.

I ended up trying different baud rates and powering down and up, but i only ever recieved:
```
0x00
```

So not i also question the USB->UART board i am using.

To debug this furhter, i will connect an oscilloscope to TX and check the signal.


While connected i also tried to send these packets:

Magic:
```
0x70 0x0a 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x86
```

Set louver down low:
```
0xf0 0x0a 0x34 0x34 0x00 0xa0 0x5c 0x00 0x00 0x00 0x00 0x00 0xa2
```

Cool mode:
```
0xf0 0x0a 0x34 0x34 0x00 0xa0 0xfd 0x00 0x00 0x00 0x00 0x00 0x01
```

None of these had any response from the unit.

So far, the heat pump remains deaf and mostly mute to me.