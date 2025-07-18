# Pinout y conexiones del termo con el ESP32:

## 🔌 Salidas a relés (GPIO - salida digital)
Rele1 → GPIO 22
Rele2 → GPIO 21
Rele3 → GPIO 19

## 🎛️ Entradas de botones (GPIO - entrada digital con pull-down)
Botón On/Off → GPIO 32
Botón Power → GPIO 33
Botón Temp → GPIO 25

## 🔆 Salidas a LEDs (Anodo común con resistencia de 100 Ω a +5V)
LED Rojo 1 (SINGLE Power) → GPIO 26
LED Rojo 2 (DOUBLE Power) → GPIO 27
LED Verde → GPIO 14

## 🌡️ Sensores de temperatura One-Wire Dallas DS18B20
DALLAS (Digital) → GPIO 04
⚠️ Resistencias pull-up de 4.7kΩ a 3.3 V

## 🔔 Buzzer (activo, control por transistor)
Control buzzer → GPIO 16

## 🧭 Sensor de orientación (tipo SW, como un botón)
Sensor nivel → GPIO 17 (entrada digital con pull-down de 3 kΩ)

## 📺 Pantalla OLED SSD1306 0.96" I2C (128x64 px)
SDA → GPIO 18
SCL → GPIO 23


