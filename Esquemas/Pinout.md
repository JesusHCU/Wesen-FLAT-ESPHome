# Pinout y conexiones del termo con el ESP32:

## 🔌 Salidas a relés (GPIO - salida digital)
Rele1 → GPIO 22

Rele2 → GPIO 21

Rele3 → GPIO 19

## 🎛️ Entradas de botones (GPIO - entrada digital con pull-down)
Botón UP → GPIO 32

Botón DOWN → GPIO 33

Botón OK → GPIO 25

## 🔆 Salidas a LEDs (Anodo común con resistencia de 100 Ω a +5V)
LED Rojo 1 (SINGLE Power) → GPIO 26

LED Rojo 2 (DOUBLE Power) → GPIO 27

LED Verde → GPIO 14

## 🌡️ Sensores de temperatura
NTC1 (analógica) → GPIO 36 (ADC1_CH0)

NTC2 (analógica) → GPIO 39 (ADC1_CH3)

⚠️ Resistencias pull-up de 3 kΩ a 3.3 V

## 🔔 Buzzer (activo, control por transistor)
Control buzzer → GPIO 4

## 🧭 Sensor de orientación (tipo SW, como un botón)
Sensor nivel → GPIO 5 (entrada digital con pull-down de 3 kΩ)

>Verificar los pines con el modelo de ESP32
