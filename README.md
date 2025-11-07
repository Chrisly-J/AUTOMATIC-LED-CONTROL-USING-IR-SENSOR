# AUTOMATIC-LED-CONTROL-USING-IR-SENSOR
##  AIM
To design and implement a system using the **STM32 microcontroller** where an LED automatically turns ON or OFF based on the input from an **IR sensor**.

---

##  Components Required
- STM32 Nucleo or Discovery Board (e.g., **Nucleo-G071RB**)
- IR Sensor Module
- LED (5mm Green or any color)
- Jumper wires
- Breadboard

---

##  Theory
An **IR sensor** detects the presence of an object by emitting and receiving infrared light.

### IR Sensor Behavior
- When an **object is detected**, the IR sensor output goes **LOW (0V)**.
- When **no object is detected**, the output stays **HIGH (3.3V)**.

### Microcontroller Response
- If **IR output = LOW** → **LED ON**
- If **IR output = HIGH** → **LED OFF**
### **Procedure**

1. Open **STM32CubeIDE**.
<img width="450" height="450" alt="Screenshot (55)" src="https://github.com/user-attachments/assets/6d9f222e-0c6b-4802-b273-dd817c3f88a8" />

  
2. Click **File → New STM32 Project**.

 <img width="450" height="450" alt="Screenshot (57)" src="https://github.com/user-attachments/assets/d2d5dc2c-35fd-433b-be65-292e24710c44" />
<img width="450" height="450" alt="Screenshot (59)" src="https://github.com/user-attachments/assets/0c228fde-d69e-47f6-ab6b-41d89a02e4e9" />

 
3. Select the **target microcontroller** or board and click **Next**.

<img width="450" height="450" alt="Screenshot (60)" src="https://github.com/user-attachments/assets/5968920a-04b8-4f3a-86c8-f817837ff768" />

4. Name the project.

   <img width="450" height="450" alt="Screenshot (61)" src="https://github.com/user-attachments/assets/b9706fa1-a47f-469b-9227-3412a6a58597" />

5. The corresponding `.ioc` file will be generated automatically.
  <img width="450" height="450" alt="Screenshot (62)" src="https://github.com/user-attachments/assets/b19331ea-463a-424b-b2b2-e992064d9f2f" />

6. Configure the pins as **GPIO (Input/Output)**, **USART**, etc. as needed.
  
<img width="450" height="450" alt="Screenshot (63)" src="https://github.com/user-attachments/assets/0e56508e-1932-4d58-8565-4e74f089532e" />

7. Save the configuration (`Ctrl + S`) – the base C program will be generated automatically.
  <img width="450" height="450" alt="Screenshot (63)" src="https://github.com/user-attachments/assets/10938b80-6ccd-4ced-af81-d2b9da927d2a" />

8. Edit the generated main program as required.
  <img width="450" height="450" alt="Screenshot (64)" src="https://github.com/user-attachments/assets/7e3aab4e-69ae-4850-8b50-a7c35946b8e9" />
<img width="450" height="450" alt="Screenshot (65)" src="https://github.com/user-attachments/assets/bbae9846-1cd4-4bed-b419-a7fc3f03a7a3" />


9. Click **Project → Build All**.

    <img width="450" height="450" alt="Screenshot (66)" src="https://github.com/user-attachments/assets/bf7a4d31-33dd-4dad-b890-57ea48368016" />

11. Link the **HEX file** using the post-build process.
   <img width="450" height="450" alt="Screenshot (67)" src="https://github.com/user-attachments/assets/cfdf0c5a-400d-4b13-852f-0e410825b571" />

12. Click **Debug** and connect the **STM Nucleo Board**.
   <img width="450" height="450" alt="Screenshot (40)" src="https://github.com/user-attachments/assets/2a9b6e93-c3ec-48ea-9da6-76fde75ef173" />

13. Click **Run** to execute the program.
    
---

### 💻 **Program**


```c
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();
    SystemClock_Config();
    MX_GPIO_Init();

    while (1)
    {
        GPIO_PinState ir = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_10); // IR OUT at PA10 (D2)

	      if (ir == GPIO_PIN_RESET)  // IR sensor HIGH = object detected
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_SET); // Turn ON LED
	      }
	      else
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_RESET); // Turn OFF LED
	      }

	      HAL_Delay(100);
    }
}
```
---
### OUTPUT
CASE 1: LED ON 
<img width="450" height="450" alt="image" src="https://github.com/user-attachments/assets/2e75abbd-5903-4f2a-8a95-7bfacc7aca4d" />

CASE 2: LED OFF
<img width="450" height="450" alt="image" src="https://github.com/user-attachments/assets/77f33307-0a59-4dac-b7a3-db40ca4b89f9" />

---
### RESULT

The experiment on IR Sensor-Based Automatic LED Control using STM32 was successfully carried out. The STM32 microcontroller accurately read the IR sensor output and controlled the LED based on object detection. When an object was detected, the LED glowed (ON) and when no object was present, the LED remained OFF. Thus, the objective of the experiment was achieved.
