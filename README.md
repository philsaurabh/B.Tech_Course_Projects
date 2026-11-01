# B.Tech Course Projects

A selection of course projects and lab work from my B.Tech at **ABV-Indian Institute of Information Technology and Management (ABV-IIITM), Gwalior**. They span embedded systems, IoT, databases, signal processing and image processing.

| Project | Area | Tools | Folder |
|---|---|---|---|
| [Embedded Systems Lab](#1-embedded-systems-lab--8051-microcontroller) | Embedded systems | 8051 assembly, Embedded C, Keil µVision | `Embedded-systems-lab-master/` |
| [Home Appliances Control System](#2-home-appliances-control-system-iot) | IoT | Arduino, HC-05 Bluetooth, Android | `Home-Automation-master/` |
| [Hostel Database System](#3-hostel-database-system) | Databases | SQL (MySQL), ER modelling | `Hostel-Database-System-master/` |
| [Digital Signal Processing Codes](#4-digital-signal-processing-codes) | Signal processing | MATLAB, C | `digital-signal-processing-codes-master/` |
| [Marker-Controlled Watershed Segmentation](#5-marker-controlled-watershed-segmentation) | Image processing | MATLAB Image Processing Toolbox | `Marker-Controlled-Watershed-Segmentation-master/` |

> Each project sits inside a nested folder of the same name, for example `Home-Automation-master/Home-Automation-master/`.

---

## 1. Embedded Systems Lab — 8051 Microcontroller

Lab experiments for the 8051 microcontroller, written in assembly and Embedded C and built with **Keil µVision**. Every experiment has its own µVision project (`.uvproj`). Build outputs are kept in `Objects/` (including the `.hex` files to flash) and `Listings/`. The full problem statements are in `practical manual.pdf`.

| # | Experiment | Language |
|---|---|---|
| 1 | Arithmetic operations: ADD, SUBB, MUL, DIV | Assembly |
| 2 | Logical operations: ANL, ORL, XRL | Assembly |
| 3 | Multiplication by repeated addition (loop with `DJNZ`) | Assembly |
| 4 | Stack operations with `PUSH` / `POP` | Assembly |
| 5–6 | Write a pattern to port P1 with a software delay | Assembly |
| 6 | LED interfacing: toggle all bits of port P1 | C |
| 7 | Display 00 to FF on port P0 | C |
| 8 | Toggle bit D0 of port P2 50,000 times | C |
| 9 | Count 0000 to 9999 on a seven-segment display | C |
| 10 | Drive a buzzer from port P1 | C |
| 11 | Rotate a stepper motor clockwise or anticlockwise | C |

**Run:** open `expN.uvproj` in Keil µVision, then build and simulate it in the debugger, or flash `Objects/expN.hex` to an 8051 board.

## 2. Home Appliances Control System (IoT)

*IoT project, 2016. Team: Alok Singh, Saurabh Sharma, Vipin Kumar, Krishna Kumar Yadav. Supervisor: Dr. Vinay Singh.*

A low-cost system to control home appliances from a smartphone. An **Arduino** receives commands over an **HC-05 Bluetooth** module from an Android phone, using a Bluetooth terminal app, and switches lights and a fan through its digital pins.

| Command | Action | Command | Action |
|---|---|---|---|
| 1 | Light 1 on | 7 | Light 1 off |
| 2 | Light 2 on | 8 | Light 2 off |
| 3 | Light 3 on | 9 | Light 3 off |
| 4 | Light 4 on | 10 | Light 4 off |
| 5 | Lights on alternately | 11 | Alternate lights off |
| 6 | Fan on | 12 | Fan off |

**Files**
- `ha.c` — main Arduino program: reads the command number from the serial port and drives pins 8–12.
- `Hacsp.ino` — alternative sketch for the DIY SmartHome Android app (lights, AC and door lock on pins 2–6), adapted from DIYhacking.com.
- `HOME APPLIANCES CONTROL SYSTEM PROJECT.pdf` — full project report (51 pages).
- `ER.png` — data model: devices, sensor data, and the commands that adjust them.

**Run:** wire the HC-05 to the Arduino's RX/TX pins, connect the loads (or LEDs) through relays to the pins listed above, and upload the sketch from the Arduino IDE. Set the serial baud rate to match your Bluetooth module (9600 is the HC-05 default). Then pair your phone and send the command numbers from a Bluetooth terminal app.

## 3. Hostel Database System

A relational database for managing hostels. It holds records of hostels, students, skilled and unskilled staff, visitors, student sign-in/sign-out, internet allocation and mess administration. Wardens, supervisors and security officers can look up and update this information.

**Design**
- **ER model** (`ER.png`), normalised into **13 tables**: `STUDENT`, `ADDRESS`, `HOSTEL`, `S_EMPLOYEE`, `U_EMPLOYEE`, `STUDENT_IN_OUT`, `VISITOR`, `INTERNET`, `MESS_ADMIN`, `MESS_MENU`, and three transaction tables (`S_EMPLOYEE_TRAN`, `U_EMPLOYEE_TRAN`, `STUDENT_TRAN`) for attendance and current allocation.
- Composite attributes (name, address) and multivalued ones (contact numbers) are decomposed. The mess is split into `MESS_ADMIN` and `MESS_MENU` to remove redundancy.

**Files**
- `hostel query.txt` — SQL to create the `HOSTELS` database and its 13 tables, insert sample records, and run example queries.
- `ER.png` — entity–relationship diagram.

**Run:** paste the statements from `hostel query.txt` into a MySQL client in order:

```sql
CREATE DATABASE HOSTELS;
USE HOSTELS;
-- then the CREATE TABLE, INSERT and SELECT statements from the file
```

## 4. Digital Signal Processing Codes

MATLAB scripts (plus one C program) from the DSP lab, covering the basic signal operations:

- **Elementary signals:** unit impulse, unit step, ramp, exponential, sinusoidal and signum signals
- **Signal operations:** reversal, addition, subtraction and multiplication (with and without loops), ramp to unit step
- **Convolution:** linear convolution (MATLAB, and in C without library functions), circular convolution (including signals of different lengths), convolution of impulses, steps and ramps
- **Transforms:** 8-point DFT; 128- and 256-point DTFT; DFT magnitude, phase and unwrapped phase plots

**Run:** open any `.m` file in MATLAB (or GNU Octave) and run it. Compile the C program with `gcc "convolution without function.c" -o conv`.

## 5. Marker-Controlled Watershed Segmentation

A MATLAB implementation of marker-controlled watershed segmentation, which separates touching objects in an image. It follows the [MathWorks example](https://in.mathworks.com/help/images/marker-controlled-watershed-segmentation.html):

1. Compute the gradient magnitude as the segmentation function.
2. Mark the foreground objects with morphological opening and closing by reconstruction, then take the regional maxima.
3. Mark the background with a distance transform and a watershed of it.
4. Impose the markers on the gradient with `imimposemin` and apply `watershed`.
5. Show the label matrix overlaid on the original image.

**Run:** put your image in the same folder, change `imread('xyz.png')` in `mask_watershed.m` to your file name, and run the script. It needs the Image Processing Toolbox.

---

## Requirements at a glance

| Project | Software | Hardware (optional) |
|---|---|---|
| Embedded Systems Lab | Keil µVision (C51) | 8051 development board |
| Home Appliances Control | Arduino IDE, Bluetooth terminal app | Arduino, HC-05, relays / LEDs |
| Hostel Database | MySQL (or MariaDB) | — |
| DSP Codes | MATLAB or GNU Octave, a C compiler | — |
| Watershed Segmentation | MATLAB + Image Processing Toolbox | — |

## License

Each project folder contains its own `LICENSE` file (© 2020 Saurabh Sharma, permissive MIT-style terms). The Marker-Controlled Watershed project adapts a MathWorks documentation example. `Hacsp.ino` is adapted from a DIYhacking.com tutorial.

## Author

**Saurabh Sharma** — B.Tech, ABV-IIITM Gwalior
