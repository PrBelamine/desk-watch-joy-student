# Desk Watch JOY STUDENT

[Français](README.md) | **English**

A desktop console for students, built around an **Arduino UNO R3 and Grove modules** and controlled with one joystick. It provides temperature and humidity readings, a Pomodoro timer, counter, stopwatch, alarm, dice, chess clock and melodies. Modules connect using Grove cables, with no soldering required.

**[MiniTech Club: project tutorial, assembly, guides and USB installer](https://minitech.club/desk-watch-joy-student/)**

## Install from MiniTech Club

Open the [Install and test section](https://minitech.club/desk-watch-joy-student/#programme) in **Chrome or Edge on a computer**.

1. Choose **Français** or **English** at the top of the page. This also selects the language of the installed program.
2. Connect your **Arduino UNO R3 (ATmega328P)** with a USB cable that supports data. Close the Arduino IDE and its Serial Monitor.
3. Click **Install JOY STUDENT** and select your board's serial port.
4. Keep the USB cable connected until installation and verification are complete.
5. When the console restarts, **leave the joystick untouched** while its resting position is calibrated.
6. Check the display, joystick, SHT readings, RTC time and buzzer before closing the enclosure.

This method requires no Arduino IDE or library installation. It replaces the program currently on the board. The installer targets the **UNO R3**, not the UNO R4. Firefox, Safari and phone browsers are not supported by this installation page.

## Modify the program with the Arduino IDE

The commented sketches are available in two languages:

- [English sketch](Desk_Watch_JOY_STUDENT_Edition_EN/Desk_Watch_JOY_STUDENT_Edition_EN.ino)
- [French sketch](Desk_Watch_JOY_STUDENT_Edition_FR/Desk_Watch_JOY_STUDENT_Edition_FR.ino)

Install the **Grove - LCD RGB Backlight** library. Open the sketch inside its matching folder, select **Arduino Uno** and the correct port, then upload. No other external library is required. Leave the joystick untouched during startup.

## Hardware

| Component | Connection / purpose |
|---|---|
| Arduino UNO R3 + Grove Base Shield | Controller; set the shield to 5 V |
| Grove LCD RGB Backlight V4.0 | I2C, 16 x 2 display |
| Grove SHT31 or SHT40 | I2C, address 0x44; automatic detection |
| DS1307 or DS3231 RTC | I2C, address 0x68; time, alarm and automatic night mode |
| Grove Thumb Joystick | Grove A1 socket; X on A1, Y on A2 |
| Grove Buzzer | D3 |

The RTC is required for the complete project. Without it, temperature and humidity remain usable, but the clock, alarm and automatic night mode are unavailable.

## Pages and controls

The menu contains **10 entries**: Temp & Hum, Timer, Counter, Stopwatch, Alarm, Dice, Chess clock, Melody, Settings and Sleep mode. **Favorite** is selected in Settings and determines the startup page.

| Action | Effect |
|---|---|
| Up / down | Scroll menus or change values; hold to repeat |
| Right or press the joystick | Confirm |
| Right or press twice within 0.4 seconds | Double-click |
| Left | Back / cancel |
| Hold left for 2.5 seconds | Sleep |
| Move during a chess game | Switch player; hold for about 1.2 seconds or press to pause |

Temp & Hum has five views: current readings, minimum, maximum, average over the last 30 readings, and automatic cycling every 3 seconds. Settings include brightness, five volume levels, startup sound, automatic sleep, night mode, RTC time, favorite and factory reset. Startup sound is off by default on a new or reset board.

## Guides and project links

| Resource | English | Français |
|---|---|---|
| Assembly guide | [PDF](docs/EN_Desk_Watch_JOY_STUDENT_Assembly_Guide.pdf) | [PDF](docs/FR_Desk_Watch_JOY_STUDENT_Guide_de_montage.pdf) |
| User guide | [PDF](docs/EN_Desk_Watch_JOY_STUDENT_User_Guide.pdf) | [PDF](docs/FR_Desk_Watch_JOY_STUDENT_Mode_d_emploi.pdf) |
| Wiring diagram | [Image](docs/wiring_EN.png) | [Image](docs/wiring_FR.png) |

- [MiniTech Club: tutorial and USB installer](https://minitech.club/desk-watch-joy-student/)
- [Support form at the bottom of the project page](https://minitech.club/desk-watch-joy-student/#support)
- [MakerWorld: printable enclosure and print profiles](https://makerworld.com/models/3490181)
- [Hackster: project write-up](https://www.hackster.io/Pr_Belamine_Makerlab/desk-watch-joy-student-arduino-uno-joystick-console-dcf03f)

## Validation and limitations

A first console was printed, assembled and tested on a real board. Hardware testing of earlier firmware does not establish complete validation of every subsequent revision or of the browser upload route.

The SHT31/SHT40 detection logic has been tested on a simulated I2C bus. **The SHT40 has not been tested on the assembled console**; its physical fit and on-device detection remain unverified. This firmware expects the sensor at address 0x44.

See the [French technical notes](README.md) for the dated build figures, hardware checks and remaining validation work.

## License

The sketches are released under the [GNU General Public License v3.0](LICENSE).
