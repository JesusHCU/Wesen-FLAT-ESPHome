# Wesen-FLAT-ESPHome

El objetivo del proyecto es hacer inteligente el termo para poder controlarlo desde Home Assistant, aprovechando parte de la electrónica del mismo.

EL termo tiene 2 placas electrónicas, una para la parte de "Potencia" y otra para la parte de "Control".

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


## 🔧 Lógica estructurada del sistema de control de termo con ESPHome

Este sistema utiliza el componente `climate.thermostat` de ESPHome para controlar dos tanques de agua de forma independiente, 
integrando un modo TURBO (Rele3), botones físicos y una interfaz visual OLED.
---

### ⚙️ Variables globales
~~~

enum PowerState {
  OFF,
  T1_ON,
  T1_T2_ON,
  T1_T2_TURBO
};

PowerState power_state = OFF
int termostato_seleccionado = 1 // 1 = T1, 2 = T2
float temp_min = 35.0
float temp_max = 75.0
float paso_temp = 5.0
~~~

### 🔘 BOTÓN 1: Encendido / Ciclo de estado
~~~
// Ciclo de estado entre OFF → T1_ON → T1_T2_ON → T1_T2_TURBO → OFF
si botón1_presionado:
  si power_state == OFF:
    power_state = T1_ON
  sino si power_state == T1_ON:
    power_state = T1_T2_ON
  sino si power_state == T1_T2_ON:
    power_state = T1_T2_TURBO
  sino:
    power_state = OFF
~~~

### 🔘 BOTÓN 2: Selección de termostato (T1 o T2)
~~~
si botón2_presionado:
  termostato_seleccionado = (termostato_seleccionado == 1) ? 2 : 1
~~~

### 🔘 BOTÓN 3: Subir temperatura del termostato seleccionado
~~~
si botón3_presionado:
  si termostato_seleccionado == 1:
    T1.target += paso_temp
    si T1.target > temp_max:
      T1.target = temp_min
  sino:
    T2.target += paso_temp
    si T2.target > temp_max:
      T2.target = temp_min
~~~

### 🔁 Lógica de activación de relés (implícita en climate.thermostat)
~~~
- T1 siempre activa rele1 cuando necesita calentar.
  Si el modo es T1_T2_TURBO, también se activa rele3 con T1.
- T2 activa rele2 de forma independiente.
  En estado OFF, todos los relés se apagan.
~~~

### 💡 Display OLED
~~~
El display muestra:
- Temperatura actual y objetivo de T1 y T2
- Indicador de tanque seleccionado
- Icono de estado Wi-Fi (con barras como en un móvil)
~~~

### 💬 Control desde Home Assistant
~~~
- Ambos termostatos pueden controlarse desde la interfaz de HA.
- El modo TURBO se puede activar desde HA ajustando la variable power_state a T1_T2_TURBO.
~~~


























