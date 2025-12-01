# EXPERIMENT 03: INTERFACING DIGITAL SENSOR WITH EDGE DEVELOPMENT BOARD  

---

### **NAME:** Vishal S
### **DEPARTMENT:** B.E. CSE (IoT)  
### **ROLL NO:** 212223110063
### **DATE OF EXPERIMENT:** 

---

## **AIM**  
To interface a **DHT22 Temperature and Humidity Sensor** with the **Raspberry Pi Pico** and display the sensor readings using **MicroPython**.  

---

## **APPARATUS REQUIRED**  
1. Raspberry Pi Pico  
2. DHT22 Temperature & Humidity Sensor  
3. 10kΩ Pull-up Resistor (if required)  
4. Jumper Wires  
5. Breadboard  
6. USB Cable  
7. Computer with Thonny IDE  

---

## **THEORY**  

### **Raspberry Pi Pico**  
Raspberry Pi Pico is a **microcontroller board** based on the **RP2040 chip**.  

- Dual-core ARM Cortex-M0+ processor  
- 26 multi-function GPIO pins  
- Supports **MicroPython** and **C/C++**  
- Interfaces: **I2C, SPI, UART, PWM**  
- Low power consumption → ideal for **IoT applications**  

### **DHT22 Sensor**  
The **DHT22** is a digital **temperature & humidity sensor** with the following features:  

- **Operating Voltage:** 3.3V – 5V  
- **Temperature Range:** -40°C to 80°C (±0.5°C accuracy)  
- **Humidity Range:** 0% – 100% (±2–5% accuracy)  
- **Data Format:** Single-wire communication protocol  

**Working Principle:**  
- Temperature → measured using a **thermistor**  
- Humidity → measured using a **capacitive sensor**  
- Data → transmitted digitally and decoded by the **MicroPython `dht` library**  

---

## **WORKING PRINCIPLE**  
1. Connect the **DHT22 sensor** to the **Raspberry Pi Pico**.  
2. Pico reads **temperature and humidity values** via a single-wire protocol.  
3. Data is **processed and displayed** on the serial monitor.  
4. If values **cross threshold limits**, an **LED alert** can be triggered.  

---

## **CIRCUIT DIAGRAM**  
<img width="667" height="520" alt="image" src="https://github.com/user-attachments/assets/32c6b5a7-5be5-4b2f-bc77-0078d127b84e" />

### **Connections:**  

| **DHT22 Pin** | **Raspberry Pi Pico Pin** |
|---------------|----------------------------|
| VCC (Pin 1)   | 3.3V or 5V                 |
| Data (Pin 2)  | GP15 (or GP28 in program)  |
| GND (Pin 4)   | GND                        |
| *(Optional)*  | 10kΩ Pull-up Resistor between **VCC & Data** |

---

## **PROGRAM (MicroPython)**  

```python
import machine
import dht
import time

# Define DHT sensor pin
dht_pin = machine.Pin(28)
dht_sensor = dht.DHT22(dht_pin)

while True:
    try:
        # Measure temperature and humidity
        dht_sensor.measure()
        temperature_celsius = dht_sensor.temperature()
        humidity_percent = dht_sensor.humidity()

        # Print results
        print("Temperature: {:.2f} °C".format(temperature_celsius))
        print("Humidity: {:.2f} %".format(humidity_percent))

    except Exception as e:
        print("Error reading DHT:", str(e))

    time.sleep(1)  # delay 1 second between readings
```

## **OUTPUT**  

The **serial monitor** displays the real-time **temperature and humidity** values as shown below:  
<img width="275" height="319" alt="image" src="https://github.com/user-attachments/assets/4e10993c-41cf-4fc4-bba2-e110dac3c48f" />



## **RESULT**  
The **DHT22 sensor** was successfully interfaced with the **Raspberry Pi Pico**, and real-time **temperature & humidity data** were displayed on the serial monitor.  
Additionally, the system worked as expected, and the **alert mechanism (LED trigger)** can be implemented for threshold crossing events.  
