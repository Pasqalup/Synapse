# STM32F405 Master Code
## Dependencies
1. Install [STM32duino](https://github.com/stm32duino/Arduino_Core_STM32) core into Arduino IDE
2. Select Generic STM32F4 Series under Tools>Board>STM32 MCU Based Boards > Generic STM32F4 Series
3. Select Generic STM32F405RGTx under Tools>Board part number>STM32F405RGTx
4. Install [Adafruit Neopixel](https://github.com/adafruit/Adafruit_NeoPixel)
## Use
1. Define all your slave info at around line 143-150 with SlaveInfo:
```
typedef struct{
  uint8_t bus; // which bus the slave is on, 1-4
  uint8_t id; // slave's ID
  uint8_t type; // type of slave, can be used to determine what commands to send
  bool active; // whether the slave is working. Initialize as false.
} SlaveInfo;
```
2. Coming soon!
