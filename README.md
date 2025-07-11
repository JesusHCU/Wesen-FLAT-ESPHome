# Wesen-FLAT-ESPHome
<img 
  src="https://github.com/JesusHCU/Wesen-FLAT-ESPHome/blob/main/Images/wesen_logo.webp"
  alt="Logo Wesen" 
  width="10%" height="auto">
Termostato para termo Wesen Flat utilizando ESPHome. 

El objetivo del proyecto es hacer inteligente el termo para poder controlarlo desde Home Assistant, aprovechando parte de la electrónica del mismo termo.

EL termo tiene 2 placas electrónicas, una para la parte de "Potencia" y otra para la parte de "Control"

## Etapa de Potencia
- Transformador y estabilizador de 5v
- 3 Relés con su circuito de activación (Resistencia, transistor y diodo)
- Conector de 5 pines para la etapa de control
- Salidas de 230v para las resistencias.
- Entrada de 230V general

## Etapa de Control
<img 
  src="https://github.com/JesusHCU/Wesen-FLAT-ESPHome/blob/main/Images/Placa%20Control%20Original.jpg" 
  alt="Cto Original" 
  width="70%" height="auto">

* Conector de 5 pines. 
  -  1- +5v
  -  2- GND
  -  3- Relé 1
  -  4- Relé 2
  -  5- Relé 3
* Conector de 2 Pines Cable Negro: Sonda NTC
* Conector de 2 Pines Cable Rojo:  Sonda NTC

<img   
  src="https://github.com/JesusHCU/Wesen-FLAT-ESPHome/blob/main/Images/Cto%20Original.jpg" 
  alt="Pistas de la placa Original" 
  width="70%" height="auto">


## Pseudocódigo estructurado para las funciones que queremos:

🔧 Variables globales:
~~~
bool termo_encendido = false
enum modo_power = SINGLE // puede ser SINGLE o DOUBLE
float temp_deseada = 35.0 // rango 35 °C–75 °C en pasos de 5
const float temp_min = 35.0
const float temp_max = 75.0
const float paso_temp = 5.0
~~~

🔘 BOTÓN 1: ON/OFF (Toggle)
~~~
si botón 1 presionado:
  termo_encendido = !termo_encendido
~~~

🔘 BOTÓN 2: Cambiar modo potencia
~~~
si botón 2 presionado:
  si modo_power == SINGLE:
    modo_power = DOUBLE
  sino:
    modo_power = SINGLE
~~~

🔘 BOTÓN 3: Subir temperatura
~~~
si botón 3 presionado:
  temp_deseada += paso_temp
  si temp_deseada > temp_max:
    temp_deseada = temp_min
~~~
🔁 LÓGICA de TERMOSTATOS (sólo si termo_encendido)
~~~
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
~~~ 
~~~
