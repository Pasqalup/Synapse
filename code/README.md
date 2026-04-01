# Code
## Both
Both the master and slave share a serial buffer of size 64. That means the maximum size of a command is 64 bytes.
Both communicate using the same command scheme outlined in [commands.h](code/master/commands.h)
## Master
The master board uses an STM32F405. It is coded in Arduino IDE using STMduino core. More info on installation [here](code/master/)
### Serial
I made an "RSBus" class to handle basic receiving and transmitting over the RS485.
- During setup(), initialize the bus with bus.init()
- Wait for the serial to initialize with
```
while (!bus1.serialReady()) ;
```
During loop() you must keep in mind several things:
- Call bus.handle() every loop
- Keep loop blocking minimal - make sure the program doesn't "hang" in the middle of a loop. Use state machines and flags instead, so the loop can keep running.
- bus.startSending() does NOT guarantee transmission is finished. You cannot make another transmission until bus.isBusy() is false.
- It is safe to call bus.startSending() while receiving; RSBus will automatically wait until it is finished recieving before transmitting
- bus.hasResponse() returns `true` if there is received data that hasn't been read yet. bus.getResponse() will clear this.

## Slave
Coding the slave is much simpler.    
- Towards the end of the main loop, you will find case PROCESSING. The slave's only job is to receive the command and respond immediately if required.
- Still keep in mind that blocking the loop is prohibited - data can be lost if the loop is slow.
- Refer to [commands.h](code/master/commands.h) for a list of commands and expected responses.
