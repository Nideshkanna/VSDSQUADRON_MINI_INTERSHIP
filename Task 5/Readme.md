Here's a `README.md` file for your 3-to-8 Decoder project:

---

# 3-to-8 Decoder Using VSDSquadron Mini

## Overview
This project involves creating a 3-to-8 decoder using the VSDSquadron Mini development board, push buttons for input, and LEDs for output. A decoder circuit activates one of eight outputs based on three binary inputs. The circuit is implemented to demonstrate practical applications of digital logic and microcontroller programming.

## Components Required
- **VSDSquadron Mini**: 1
- **Push Buttons** (for binary inputs): 3
- **LEDs** (for outputs): 8
- **Breadboard**: 1
- **Jumper Wires**: 20-30
- **PlatformIO IDE** (for software development)

## Circuit Connection
1. **Inputs**: Connect three push buttons to GPIO input pins on the VSDSquadron Mini.
2. **Outputs**: Connect eight LEDs to GPIO output pins on the VSDSquadron Mini.
3. **Power and Ground**: Ensure a common ground and proper power supply for all components.
4. **Wiring**: Use jumper wires to establish the connections according to the pinout.

### Pinout Table
| **Input Name** | **Pin Number on VSDSquadron Mini** |
| -------------- | ----------------------------------- |
| A              | PD1                                 |
| B              | PD2                                 |
| C              | PD3                                 |

| **Output Name** | **Pin Number on VSDSquadron Mini** |
| --------------- | ----------------------------------- |
| Y0              | PC1                                 |
| Y1              | PC2                                 |
| Y2              | PC3                                 |
| Y3              | PC4                                 |
| Y4              | PC5                                 |
| Y5              | PC6                                 |
| Y6              | PC7                                 |
| Y7              | PC8                                 |

## Truth Table for 3-to-8 Decoder
| **A** | **B** | **C** | **Output** (Active) |
|-------|-------|-------|---------------------|
| 0     | 0     | 0     | Y0                  |
| 0     | 0     | 1     | Y1                  |
| 0     | 1     | 0     | Y2                  |
| 0     | 1     | 1     | Y3                  |
| 1     | 0     | 0     | Y4                  |
| 1     | 0     | 1     | Y5                  |
| 1     | 1     | 0     | Y6                  |
| 1     | 1     | 1     | Y7                  |

## How to Program
1. Install PlatformIO in VS Code.
2. Connect the VSDSquadron Mini board to your computer.
3. Write and upload the following code using PlatformIO:

```c
#include <stdio.h>
#include <ch32v00x.h>

// Function for GPIO Configuration
void GPIO_Config(void) {
    GPIO_InitTypeDef GPIO_InitStructure = {0};
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);
    
    // Input Pins Configuration (PD1, PD2, PD3)
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
    GPIO_Init(GPIOD, &GPIO_InitStructure);

    // Output Pins Configuration (PC1-PC8)
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3 | GPIO_Pin_4 |
                                  GPIO_Pin_5 | GPIO_Pin_6 | GPIO_Pin_7 | GPIO_Pin_8;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOC, &GPIO_InitStructure);
}

int main() {
    uint8_t A, B, C;
    GPIO_Config();

    while(1) {
        A = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_1);
        B = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_2);
        C = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_3);
        uint8_t decoded_value = (A << 2) | (B << 1) | C;

        // Turn off all LEDs
        GPIO_Write(GPIOC, 0x00);

        // Activate the corresponding output
        if (decoded_value < 8) {
            GPIO_SetBits(GPIOC, (1 << decoded_value));
        }
    }
}
```

## Circuit Diagram
Ensure to create a neat digital or hand-drawn circuit diagram showing the connections between the VSDSquadron Mini board, push buttons, and LEDs.

## How It Works
- The three inputs \( A, B, C \) are read as binary values.
- The binary combination determines which output LED will be turned on.
- The logic activates only one of the eight outputs at a time based on the input.

## Applications
- Memory address decoding
- Control signal generation in microprocessor systems
- Binary-to-decimal decoders

---
