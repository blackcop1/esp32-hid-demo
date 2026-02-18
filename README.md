# ESP32 HID Security Demonstration

**Educational project showcasing HID vulnerabilities for security exhibition**

⚠️ **WARNING**: This project is for **EDUCATIONAL PURPOSES ONLY**. Unauthorized use of HID attack techniques is illegal. Only use on systems you own or have explicit permission to test.

## Overview

This project demonstrates how an ESP32 microcontroller can emulate a USB HID keyboard to execute automated commands on a Windows system. This is commonly known as a "BadUSB" or "Rubber Ducky" style attack.

## Hardware Requirements

- **ESP32-S2** or **ESP32-S3** (with native USB support)
- USB cable
- Computer running Windows

**Note**: Regular ESP32 boards do NOT support native USB HID. You MUST use ESP32-S2 or ESP32-S3.

## Software Requirements

- Arduino IDE (1.8.19 or later) OR Arduino IDE 2.x
- ESP32 Board Support Package

## Installation

### 1. Install Arduino IDE
Download from: https://www.arduino.cc/en/software

### 2. Add ESP32 Board Support

1. Open Arduino IDE
2. Go to **File → Preferences**
3. Add this URL to "Additional Board Manager URLs":
   ```
   https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
   ```
4. Go to **Tools → Board → Boards Manager**
5. Search for "esp32"
6. Install "esp32 by Espressif Systems" (version 2.0.5 or later)

### 3. Select Your Board

1. Go to **Tools → Board → ESP32 Arduino**
2. Select either:
   - **ESP32S2 Dev Module** (for ESP32-S2)
   - **ESP32S3 Dev Module** (for ESP32-S3)

### 4. Configure USB Settings

- **USB Mode**: "USB-OTG (TinyUSB)" or "Hardware CDC and JTAG"
- **USB CDC On Boot**: "Enabled"

## Available Demos

### 1. CMD Version (`esp32_hid_demo.ino`)
Opens Command Prompt and displays repeated "SYSTEM HACKED" message in terminal window.

**Features:**
- Red text on black background
- Infinite loop displaying alert message
- Terminal-based display

### 2. GUI Version (`esp32_hid_demo_gui.ino`)
Opens PowerShell and displays repeating GUI popup message boxes.

**Features:**
- Windows Forms message box
- Infinite popup loop
- More visually impactful for demonstrations

## How to Use

### Upload to ESP32

1. Open your chosen `.ino` file in Arduino IDE
2. Connect your ESP32-S2/S3 to your computer via USB
3. Select the correct **Port** under **Tools → Port**
4. Click **Upload** button
5. Wait for upload to complete

### Execute Demonstration

1. **Unplug** the ESP32 from your computer
2. **Plug it back in** to a Windows machine
3. Wait 3 seconds for initialization
4. The payload will execute automatically

### Stop the Demo

- **CMD Version**: Close the Command Prompt window or press `Ctrl+C`
- **GUI Version**: Press `Ctrl+Alt+Delete` → Task Manager → End "PowerShell" task

## How It Works

### Attack Chain

1. ESP32 enumerates as a USB HID keyboard
2. Waits 3 seconds for driver recognition
3. Simulates keyboard shortcuts:
   - Presses `Windows + R` (opens Run dialog)
   - Types command (`cmd` or `powershell`)
   - Executes scripted commands
4. Creates looping display message

### Key Components

- **USBHIDKeyboard**: Arduino library for HID keyboard emulation
- **Keyboard shortcuts**: Automates Windows navigation
- **Command injection**: Executes batch/PowerShell commands
- **Timing delays**: Ensures commands execute properly

## Educational Value

This demonstration illustrates:

- **Physical security importance**: USB ports are attack vectors
- **Supply chain risks**: Unknown USB devices are dangerous
- **Social engineering**: Devices can appear harmless
- **Defense strategies**: USB port controls, endpoint protection

## Countermeasures

### For Organizations

1. **Disable USB ports** on sensitive systems
2. Implement **USB device whitelisting**
3. Use **endpoint protection** that monitors HID activity
4. **Physical security** for workstations
5. **Employee training** on USB device risks

### For Individuals

1. **Never plug in** unknown USB devices
2. Use **USB data blockers** for charging
3. Keep systems **updated** with security patches
4. Enable **screen locks** when away from computer

## Legal & Ethical Considerations

🔴 **IMPORTANT**: 

- Using this code on systems without authorization is **ILLEGAL**
- Intended for **security education and awareness** only
- Always obtain **written permission** before testing
- Use in **controlled environments** only (your own devices/lab)

## Customization

### Modify the Message

Change this line in the code:
```cpp
Keyboard.print("echo          THIS SYSTEM IS HACKED!");
```

### Change Timing

Adjust delay values (in milliseconds):
```cpp
delay(3000); // 3 second wait
```

### Add More Commands

Add additional keyboard actions:
```cpp
Keyboard.print("your command here");
Keyboard.press(KEY_RETURN);
Keyboard.releaseAll();
```

## Troubleshooting

### ESP32 Not Recognized
- Ensure you're using ESP32-S2 or ESP32-S3
- Check USB cable supports data transfer
- Try different USB port
- Install CH340/CP2102 drivers if needed

### Payload Not Executing
- Increase initial delay (line: `delay(3000);`)
- Verify USB Mode settings in Arduino IDE
- Check Windows is not blocking command execution

### Commands Typing Incorrectly
- Increase delays between commands
- Check keyboard layout matches (US layout assumed)

## Repository Structure

```
esp32-hid-demo/
├── esp32_hid_demo.ino          # CMD version
├── esp32_hid_demo_gui.ino      # GUI popup version
├── README.md                    # This file
└── LICENSE                      # License information
```

## License

MIT License - See LICENSE file for details

## Disclaimer

This project is provided "as is" for educational purposes. The authors are not responsible for any misuse or damage caused by this code. Users are solely responsible for ensuring legal and ethical use.

## Resources

- [ESP32 Arduino Documentation](https://docs.espressif.com/projects/arduino-esp32/)
- [USB HID Specification](https://www.usb.org/hid)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)

## Contributing

This is an educational project for a security exhibition. If you have suggestions for improving the educational value or security awareness aspects, feel free to open an issue.

---

**Remember**: With great power comes great responsibility. Use this knowledge to improve security, not compromise it.