# FreeRTOS_LoraWAN

The project is on a zip because it has external dependencies, it cannot be standalone.   
It's in LoRaWan-E5-Node-qian\Projects\Applications\FreeRTOS\FreeRTOS_LoRaWAN

This is the project from the seeed studio github.  
Note: **You cannot migrate this project to a new version of the CubeMX, because it will delete parts of the code.**
Plus they didn't really used the CubeMX to generate the project.

## Changes

1. For the project to compile sucessfully, in main.h the *hlptim1* declaration had the **extern** keyword added.

```c
/* USER CODE BEGIN Private defines */
extern LPTIM_HandleTypeDef hlptim1;

/* USER CODE END Private defines */
```
2. In LoraWAN/App/se-identity.h the LORAWAN_JOIN_EUI macro was changed from { 0x01, 0x01, 0x01, 0x01, 0x01, 0x01, 0x01, 0x01 } 
to { 0x01, 0x01, 0x01, 0x01, 0x01, 0x01, 0x02, 0x02 }.    
The reason is because there is already and end device and application with the default keys in Things Stack.   
The rest of the macros were left has default.   

See the **Things_Stack_Dashboard.md** file from the Wio-E5-mini-LoRa-Setup repository if you haven't yet registered an end device 
and application.

3. In main.c the led toggling in the StartLedTask() was commented out to allow for downlink testing using the RED led.

## In lora_app.c

The only changes are in the SendTxData() and OnRxData() functions. Both have comments that explain them. They are the same
as in the ST example. So the transmission is by default done by a timer.
