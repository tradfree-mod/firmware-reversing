# firmware-reversing


### OpenGDB + GDB
- Install the latest version of OpenOCD
```
git clone http://openocd.zylin.com/openocd
cd openocd
./bootstrap
./configure
make -j4
sudo make install
```

- Run OpenOCD and dump the memory

```
cd $THIS_REPO
openocd -f res/ftdi.cfg -f res/efm32.cfg

# In another terminal

telnet localhost 4444

flash read_bank 0 dump.bin
```


- Debug with gdb

```
arm-none-eabi-gdb

(gbd) target remote localhost:3333
(gdb) monitor reset halt
```

### Useful info

#### Memory map

- ROM:           0x00000000 - 0x00040000 (256kB)
- RAM:           0x20000000 - 0x20007fff (32kB)
- Peripherals: 
	- ACMP0:     0x40000000 - 0x400003ff
	- ACMP1:     0x40000400 - 0x400007ff
	- ADC0:      0x40002000 - 0x400023ff
	- IDAC0:     0x40006000 - 0x400063ff
	- GPIO:      0x4000a000 - 0x4000afff
	- I2C0:      0x4000c000 - 0x4000c3ff
	- USART0:    0x40010000 - 0x400103ff
	- USART1:    0x40010400 - 0x400107ff
	- TIMER0:    0x40018000 - 0x400183ff
	- TIMER1:    0x40018400 - 0x400187ff
	- GPCRC:     0x4001c000 - 0x4001c3ff
	- CRYOTIMER: 0x4001e000 - 0x4001e3ff
	- RTCC:      0x40042000 - 0x400423ff
	- LETIMER0:  0x40046000 - 0x400463ff


- [ARM Vector table](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.dui0552a/BABIFJFG.html)

