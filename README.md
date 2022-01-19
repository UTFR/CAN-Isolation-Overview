# CAN-Isolation Board Overview
By: Ayrton Antenucci, Electric Powertrain Design, University of Toronto Formula Racing

Each year, the University of Toronto Formula Racing Team (UTFR) designs and builds a car to compete in international Formula SAE (Formula Student) events. As such, the team must ensure all elements of the vehicle, including the electric powertrain, comply entirely with Formula SAE regulations. This article will discuss the team’s first CAN-Isolation board, including its purpose, functionality, and design. All of UTFR’s boards are fabricated in collaboration with JLCPCB (www.jlcpcb.com), a leading PCB manufacturer providing high quality, reliable, and cost-effective PCBs at a consistently rapid pace. 

## Purpose and Functionality
    
As per Formula SAE (FSAE) regulations, all circuits susceptible to high voltage within the accumulator (Tractive System or TS circuits) must be electrically isolated from low voltage circuits grounded to the chassis (Grounded Low Voltage or GLV circuits). 

UTFR’s battery management system (BMS) is considered a GLV circuit, and must communicate over a CAN bus with thermistor modules to actively read cell temperatures. Because all thermistors are to be placed directly on busbars within the cell modules, the thermistor modules are considered TS circuits. As such, CAN signals between the thermistor modules and the BMS must be isolated to comply with FSAE regulations. This is the purpose of the CAN-isolation board.

The board achieves isolation by terminating the CAN buses from the thermistor modules and the BMS on opposite ends of the board. On both ends, messages are sent through transceivers and decoded by CAN controllers. A central Arduino Micro handles interrupts from the controllers and sends each message across to the opposite CAN bus. A galvanically-isolated CAN transceiver terminates the thermistor module CAN bus, electrically isolating the TS and GLV circuits while still enabling CAN communication across the PCB.

## Schematic and PCB Design

The CAN-Isolation PCB was designed entirely using Altium Designer. As is shown in the schematic below, the board incorporates MCP2515 CAN controllers (U2, U4), an MCP2551 transceiver on the BMS (GLV) side of the board (U1), and an ADM3053 isolating transceiver on the thermistor module (TS) side of the board (U6).

![image](https://user-images.githubusercontent.com/88075549/150188852-5e7739af-8405-4549-a807-b8eaedaa54c6.jpeg)

The board also includes a 12V DC/DC converter (U7) to provide isolated power to the thermistor modules and a 12-5V low dropout regulator (U5) to power the ADM3053 isolated transceiver. 

For debugging purposes, switches are present on both CAN bus termination circuits and several LEDs are included to monitor power and SPI communication between the controllers and the Arduino (U3). Below is the final routing diagram of the PCB, for reference.

![image](https://user-images.githubusercontent.com/88075549/150188984-66bf6de3-48dd-4378-955b-0ddc9bb43778.jpeg)

## Ordering and Fabrication

The CAN-Isolation board was manufactured with exceptional quality by JLCPCB within days of ordering. If desired, JLCPCB also offers SMT assembly with just a 24h turnaround time. The ordering process is remarkably simple:

  1) Export Gerber files of PCB project
  2) Click ‘Order Now’ on www.jlcpcb.com
  3) Upload Gerber files, confirm generated PCB requirements and preferences
  4) Once all PCBs are saved to cart, proceed to checkout.
