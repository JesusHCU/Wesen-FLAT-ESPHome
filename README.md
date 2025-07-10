# Wesen-FLAT-ESPHome
Termostato para termo Wesen Flat utilizando ESPHome

El objetivo del proyecto es hacer inteligente el termo para poder controlarlo desde Home Assistant, aprovechando parte de la electrónica del mismo termo.

## Peudocódigo estructurado para las funciones que queremos:

🔧 Variables globales:
bool termo_encendido = false
enum modo_power = SINGLE // puede ser SINGLE o DOUBLE
float temp_deseada = 35.0 // rango 35 °C–75 °C en pasos de 5
const float temp_min = 35.0
const float temp_max = 75.0
const float paso_temp = 5.0

🔘 BOTÓN 1: ON/OFF (Toggle)
si botón 1 presionado:
  termo_encendido = !termo_encendido
  
🔘 BOTÓN 2: Cambiar modo potencia
si botón 2 presionado:
  si modo_power == SINGLE:
    modo_power = DOUBLE
  sino:
    modo_power = SINGLE

🔘 BOTÓN 3: Subir temperatura
si botón 3 presionado:
  temp_deseada += paso_temp
  si temp_deseada > temp_max:
    temp_deseada = temp_min

🔁 LÓGICA de TERMOSTATOS (sólo si termo_encendido)
si termo_encendido:
  si temperatura_tanque1 < temp_deseada:
    si modo_power == DOUBLE:
      activar rele1 y rele3
    sino:
      activar rele1
  sino:
    desactivar rele1 y rele3

  si temperatura_tanque2 < temp_deseada:
    activar rele2
  sino:
    desactivar rele2
    
