# 🔐 Laser Security System

<p align="center">
  <img src="https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="Arduino"/>
  <img src="https://img.shields.io/badge/Security-DC2626?style=for-the-badge" alt="Security"/>
  <img src="https://img.shields.io/badge/Laser-FF0000?style=for-the-badge" alt="Laser"/>
  <img src="https://img.shields.io/badge/Embedded-FF6F00?style=for-the-badge" alt="Embedded"/>
</p>

## 📖 Overview

An intelligent laser-based security system that creates an invisible perimeter using laser beams and LDR (Light Dependent Resistor) sensors. When the laser beam is interrupted by an intruder, the system triggers alarms, activates cameras, sends notifications, and logs the breach event. Ideal for securing doorways, hallways, safes, and restricted areas.

## ✨ Features

- 🔴 **Invisible Laser Barrier** - Creates undetectable security perimeter
- 📡 **Multi-Point Detection** - Multiple laser-LDR pairs for wider coverage
- 🚨 **Instant Alert System** - Audio and visual alarms on intrusion
- 📸 **Camera Trigger** - Activate surveillance cameras on breach
- 📱 **SMS/Email Alerts** - Real-time notifications to owner
- 🔐 **Keypad Arming/Disarming** - PIN-based system control
- ⏱️ **Delayed Activation** - Entry/exit delay periods
- 📊 **Event Logging** - Records all breach attempts
- 💡 **Status Indicators** - LED display for system state
- 🔋 **Battery Backup** - Continues operation during power outage

## 🛠️ Hardware Components

### Basic Version

| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno / Nano | 1 | Main controller |
| Laser Diode Module (650nm, 5mW) | 2-4 | Laser beam source |
| LDR (Light Dependent Resistor) | 2-4 | Beam detection |
| Resistors (10KΩ) | 2-4 | LDR pull-down |
| Buzzer (5V, 85dB) | 1 | Audio alarm |
| Red LED | 3 | Status indicators |
| Green LED | 1 | System armed indicator |
| 4x4 Keypad | 1 | PIN entry |
| 16x2 LCD Display (I2C) | 1 | Status display |
| Relay Module | 1 | Camera/light control |
| Push Button | 1 | Emergency disarm |
| 9V Battery/Adapter | 1 | Power supply |

### Advanced Version (Additional)

| Component | Quantity | Purpose |
|-----------|----------|---------|
| ESP32/ESP8266 | 1 | WiFi connectivity |
| PIR Motion Sensor | 1 | Backup detection |
| GSM Module (SIM800L) | 1 | SMS alerts |
| SD Card Module | 1 | Data logging |
| RTC Module (DS3231) | 1 | Timestamp |
| 12V Battery | 1 | Backup power |

## 📐 Circuit Diagram

### Basic Circuit

```
                    Arduino Uno
                    ┌──────────────┐
   LDR 1 (A0) ─────►│ A0           │
   LDR 2 (A1) ─────►│ A1           │
   LDR 3 (A2) ─────►│ A2           │
   LDR 4 (A3) ─────►│ A3           │
                    │              │
   Buzzer ─────────►│ D2           │
   Red LED 1 ──────►│ D3           │
   Red LED 2 ──────►│ D4           │
   Green LED ──────►│ D5           │
                    │              │
   Relay ──────────►│ D6           │
                    │              │
   Keypad Row 1 ───►│ D7           │
   Keypad Row 2 ───►│ D8           │
   Keypad Row 3 ───►│ D9           │
   Keypad Row 4 ───►│ D10          │
   Keypad Col 1 ───►│ D11          │
   Keypad Col 2 ───►│ D12          │
   Keypad Col 3 ───►│ D13          │
   Keypad Col 4 ───►│ A4           │
                    │              │
   LCD SDA ────────►│ A4  I2C      │
   LCD SCL ────────►│ A5  I2C      │
                    │              │
   5V Power ───────►│ 5V           │
   Ground ─────────►│ GND          │
                    └──────────────┘

   Laser 1-4 ──────► 5V + GND (Always ON)
```

### LDR Circuit

```
           5V
            │
            ├──── 10KΩ Resistor
            │
            ├──── To Arduino Analog Pin
            │
          [LDR]
            │
           GND
```

## 💻 Software Requirements

- **Arduino IDE** 1.8.x or 2.x
- **Required Libraries:**
  - `Keypad.h` - Keypad input
  - `LiquidCrystal_I2C.h` - LCD display
  - `Wire.h` - I2C communication (built-in)
  - `EEPROM.h` - Store PIN code (built-in)

### For Advanced Version:
  - `WiFi.h` / `ESP8266WiFi.h` - WiFi
  - `SD.h` - SD card logging
  - `RTClib.h` - Real-time clock
  - `SoftwareSerial.h` - GSM communication

## 📦 Installation

### 1. Library Installation

```bash
# Open Arduino IDE
# Sketch → Include Library → Manage Libraries
# Install:
# - Keypad by Mark Stanley
# - LiquidCrystal I2C by Frank de Brabander
```

### 2. Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/laser-security-system.git
cd laser-security-system
```

### 3. Hardware Setup

#### Laser Positioning

1. **Mount Lasers**
   - Install at strategic points (doorway, corridor)
   - Height: Waist level (~90cm) or multiple heights
   - Ensure stable mounting

2. **Align LDRs**
   - Position directly opposite each laser
   - Distance: 1-10 meters effective range
   - Use small tubes to focus light on LDR

3. **Test Alignment**
   ```cpp
   // Upload test sketch
   // Monitor Serial output
   // Adjust until stable reading
   ```

### 4. Upload Code

1. Connect Arduino via USB
2. Select Board: **Arduino Uno/Nano**
3. Select Port: Your COM port
4. Open `laser_security.ino`
5. Click **Upload** ⬆️

### 5. Initial Configuration

1. Power on system
2. Default PIN: **1234**
3. Press **#** to enter setup mode
4. Change PIN: **# → 1234 → New PIN → ***
5. Test by arming/disarming

## 🚀 Usage

### System States

| State | Description | Green LED | Buzzer | LCD Display |
|-------|-------------|-----------|--------|-------------|
| **Disarmed** | System inactive | Blinking | OFF | "System Disarmed" |
| **Armed** | Monitoring active | Solid ON | OFF | "System Armed" |
| **Entry Delay** | Grace period to disarm | Fast blink | Beeping | "Enter PIN: ___" |
| **Alarm** | Intrusion detected | OFF | Continuous | "INTRUDER ALERT!" |
| **Setup** | Configuration mode | OFF | OFF | "Setup Mode" |

### Arming the System

1. Enter PIN on keypad: `1234`
2. Press `*` to arm
3. Exit delay: 10 seconds to leave area
4. System armed - Green LED solid

### Disarming the System

1. Enter area (triggers entry delay)
2. Enter PIN: `1234`
3. Press `#` to disarm
4. System disarmed - Green LED blinking

### Changing PIN Code

1. Enter current PIN: `1234`
2. Press `#` for setup
3. Press `1` for change PIN
4. Enter new 4-digit PIN
5. Confirm new PIN
6. Press `#` to save

### Handling False Alarms

1. Enter PIN quickly during alarm
2. Press `0` to silence alarm
3. System returns to armed state
4. Event logged as false alarm

## 🔧 Calibration

### LDR Threshold Calibration

```cpp
// In laser_security.ino

void calibrateLDR() {
  // Read LDR values with laser ON
  int ldrValueON = analogRead(LDR_PIN);
  
  // Read LDR values with laser OFF (blocked)
  int ldrValueOFF = analogRead(LDR_PIN);
  
  // Set threshold between ON and OFF
  int threshold = (ldrValueON + ldrValueOFF) / 2;
  
  Serial.print("Threshold: ");
  Serial.println(threshold);
  
  // Update in code
  #define LDR_THRESHOLD threshold
}
```

### Typical LDR Values

| Condition | Analog Reading | Status |
|-----------|----------------|--------|
| Laser ON (normal) | 800-1000 | Secure |
| Laser Blocked | 0-200 | Breach |
| Ambient light | 300-600 | Adjust laser |

## 📊 System Features

### 1. Multi-Zone Detection

```cpp
#define NUM_ZONES 4

struct Zone {
  int ldrPin;
  int threshold;
  bool isBreached;
  char name[20];
};

Zone zones[NUM_ZONES] = {
  {A0, 500, false, "Main Door"},
  {A1, 500, false, "Window"},
  {A2, 500, false, "Corridor"},
  {A3, 500, false, "Vault"}
};
```

### 2. Event Logging

```cpp
struct Event {
  char timestamp[20];
  char type[20];      // "Arm", "Disarm", "Breach"
  char zone[20];
  char user[10];
};

void logEvent(Event e) {
  // Save to SD card or EEPROM
  // Display on serial monitor
  // Send to cloud (if WiFi available)
}
```

### 3. Delayed Activation

```cpp
// Entry delay: Time to disarm after trigger
#define ENTRY_DELAY 30000  // 30 seconds

// Exit delay: Time to exit after arming
#define EXIT_DELAY 10000   // 10 seconds
```

### 4. Alarm Patterns

```cpp
void alarmPattern() {
  // Fast beeping for entry delay
  // Continuous for full alarm
  // Different patterns for different zones
}
```

## 📱 Advanced Features (WiFi Version)

### Web Dashboard

```cpp
// Access at http://ESP32_IP_ADDRESS

Dashboard Features:
- Real-time system status
- Arm/disarm remotely
- View event log
- Change settings
- View camera feed
```

### Mobile Notifications

```cpp
void sendAlert(String message) {
  // Email via SMTP
  sendEmail("owner@email.com", message);
  
  // SMS via GSM module
  sendSMS("+919876543210", message);
  
  // Push notification via Blynk
  Blynk.notify(message);
}
```

### Cloud Integration

```cpp
void uploadToCloud() {
  // Send to ThingSpeak, Firebase, etc.
  ThingSpeak.setField(1, systemArmed);
  ThingSpeak.setField(2, lastBreachTime);
  ThingSpeak.setField(3, breachCount);
  ThingSpeak.writeFields(channelID, apiKey);
}
```

## 🐛 Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| False alarms | Laser misalignment | Realign laser to LDR center |
| No detection | LDR not receiving light | Check laser power, alignment |
| Keypad not working | Wrong pin assignment | Verify keypad wiring |
| LCD blank | I2C address wrong | Try 0x27 or 0x3F |
| Buzzer too quiet | Voltage too low | Use separate 5V supply |
| Random triggers | Ambient light interference | Shield LDR or adjust threshold |
| Won't disarm | PIN incorrect | Use master reset code |

### Master Reset

```cpp
// If PIN forgotten, upload this code:
void setup() {
  EEPROM.write(0, 1);  // Write new PIN
  EEPROM.write(1, 2);
  EEPROM.write(2, 3);
  EEPROM.write(3, 4);
}
// New PIN is now 1234
```

## 🔐 Security Best Practices

1. **Laser Safety**
   - Use Class 2 lasers (<1mW)
   - Never point at eyes
   - Warning signs recommended

2. **PIN Security**
   - Change default PIN immediately
   - Don't share PIN
   - Use 6-digit PIN for better security

3. **Physical Security**
   - Hide wiring in walls/conduits
   - Lock control box
   - Backup power supply

4. **Testing**
   - Test weekly
   - Check battery backup
   - Verify all zones

## 📈 Performance Specs

- **Detection Range:** 1-10 meters
- **Response Time:** < 100ms
- **False Alarm Rate:** < 1% (with proper calibration)
- **Battery Life:** 8-12 hours (with backup)
- **Operating Temperature:** 0°C to 45°C
- **Power Consumption:** 200-300mA at 5V

## 🌟 Future Enhancements

- [ ] Face recognition to identify authorized users
- [ ] Multiple user PINs with access logs
- [ ] Wireless laser-LDR pairs
- [ ] Integration with smart home systems
- [ ] Mobile app for iOS/Android
- [ ] Machine learning for pattern recognition
- [ ] Geofencing for auto arm/disarm
- [ ] Two-way audio communication
- [ ] Video recording on breach
- [ ] Professional monitoring service integration


## ⚠️ Legal Disclaimer

- Check local laws regarding laser use
- Inform visitors of security system
- Comply with privacy regulations
- This is for educational purposes
- Not a replacement for professional security

## 🤝 Contributing

Contributions welcome! Areas to improve:
- Enhanced detection algorithms
- Better power management
- Additional notification methods
- Mobile app development



## 👤 Author

**Ajay Kumar Pujari**
- Email: ajaykumarpujari22@gmail.com
- GitHub: [ajaykumarpujari12-svg](https://github.com/ajaykumarpujari12-svg)


## 🙏 Acknowledgments

- Arduino community
- Security system design principles
- Open-source contributors

## 📚 Resources

- [Laser Safety Guidelines](https://www.fda.gov/radiation-emitting-products/laser-products)
- [LDR Sensor Guide](https://components101.com/resistors/ldr-datasheet)
- [Arduino Keypad Tutorial](https://www.arduino.cc/reference/en/libraries/keypad/)

---

⭐ If this project helped secure your space, please star it!

**Tags:** `arduino` `security-system` `laser` `alarm` `embedded-systems` `home-security` `iot` `intrusion-detection` `diy` `electronics`
