# STM32 Sound-Activated Switch

A real-time sound-controlled lighting system built on the STM32L476VG microcontroller. The system continuously monitors ambient audio via an analog sound sensor, and toggles an LED every time a sound event (such as a clap) exceeds a calibrated threshold. Built for CENG 315 at the American University of Ras Al Khaimah.

![STM32L476 Discovery Board](https://www.st.com/content/ccc/fragment/product_related/rpn_information/board_photo/group0/1b/7f/ef/a8/6a/35/43/1c/um1879-discovery-kit-with-stm32l476vg-mcu-stmicroelectronics/files/um1879.jpg/jcr:content/translations/en.um1879.jpg)

## Demo

Clap once → LED turns ON. Clap again → LED turns OFF. Response time under 10ms.

## Hardware

| Component | Details |
|---|---|
| Microcontroller | STM32L476VG (ARM Cortex-M4, 80MHz) |
| Board | STM32L476G-DISCO Discovery Kit |
| Sound Sensor | DFRobot Gravity Analog Sound Sensor |
| IDE | STM32CubeIDE |

## Pin Connections

| Sensor Pin | STM32 Pin | Function |
|---|---|---|
| VCC | 3.3V | Power supply |
| GND | GND | Common ground |
| Signal | PA1 | ADC1_IN6 (analog input) |
| LED output | PB2 | GPIO output (red LED) |

## How It Works

The sound sensor outputs an analog voltage proportional to sound intensity. This is sampled by the 12-bit ADC on pin PA1, producing values between 0 and 4095. A software threshold of 1000 filters out background noise (ambient ADC readings typically range 100–300). When a clap is detected (ADC readings of 2500–3800), the LED on PB2 is toggled. A 250ms software debounce prevents multiple triggers from a single sound event.

## ADC Configuration

- Resolution: 12-bit
- Mode: Continuous conversion
- Clock: Asynchronous, divided by 1
- Sampling time: 47.5 cycles
- Data alignment: Right

## Project Structure
├── Core/
│   ├── Inc/          # Header files
│   └── Src/          # Source files (main.c, HAL config)
├── Drivers/          # STM32 HAL and CMSIS libraries
├── sensor.ioc        # STM32CubeMX configuration
└── README.md

## Performance

| Parameter | Value |
|---|---|
| Ambient ADC reading | 100 – 300 |
| Clap ADC reading | 2500 – 3800 |
| Threshold | 1000 |
| Response time | < 10ms |
| Signal return to baseline | 50 – 100ms |

## Build Instructions

1. Clone the repo
2. Open STM32CubeIDE → File → Import → Existing Project
3. Select the cloned folder
4. Build and flash to the STM32L476G-DISCO board

## Report

The full technical report including hardware calibration, register-level configuration, and oscilloscope testing is available [here](./CENG_315_Project_Report_1__Copy_.pdf).

## Course

CENG 315 — Microprocessors  
American University of Ras Al Khaimah  
Spring 2026