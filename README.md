# Wesen-FLAT-ESPHome
El objetivo del proyecto es hacer inteligente el termo para poder controlarlo desde Home Assistant, aprovechando parte de la electrónica del mismo.

![GitHub top language](https://img.shields.io/github/languages/top/JesusHCU/Wesen-FLAT-ESPHome?style=for-the-badge)
![GitHub last commit](https://img.shields.io/github/last-commit/JesusHCU/Wesen-FLAT-ESPHome?style=for-the-badge)
![GitHub repo size](https://img.shields.io/github/repo-size/JesusHCU/Wesen-FLAT-ESPHome?style=for-the-badge)

# Termo INOX Domotizado con ESPHome 🔥💧
Este proyecto transforma un termo eléctrico de doble tanque en un dispositivo inteligente totalmente integrado en **Home Assistant** mediante **ESPHome** y un microcontrolador **ESP32**. Permite un control total, monitorización y automatización avanzada para optimizar el consumo energético y el confort.




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



## ✨ Características Principales

-   **🔌 Control Total ON/OFF**: Enciende y apaga el termo de forma remota o local.
-   **🔥 Modos de Calentamiento**:
    -   **Modo 1**: Calienta solo el Tanque 1 (salida de agua caliente).
    -   **Modo 2**: Calienta ambos tanques para máxima capacidad.
    -   **Modo TURBO**: Usa una resistencia extra para calentar el Tanque 1 de forma ultrarrápida.
-   **🌡️ Control de Temperatura Independiente**: Ajusta la temperatura objetivo para cada tanque por separado.
-   **🕹️ Interfaz Física**: Controla el termo mediante 3 botones físicos para ON/OFF, cambio de modo y ajuste de temperatura.
-   **📺 Display OLED**: Una pantalla SH1106 muestra en tiempo real el estado, las temperaturas actuales y objetivo, y la calidad de la señal WiFi.
-   **🔔 Feedback Sonoro**: Un zumbador proporciona confirmaciones audibles al pulsar los botones.
-   **🏠 Integración Nativa con Home Assistant**: El dispositivo se integra a la perfección, exponiendo todas las entidades necesarias para su control y monitorización.
-   **🔄 Actualizaciones OTA**: Actualiza el firmware del ESP32 de forma inalámbrica a través de WiFi.

---

## 🛠️ Componentes y Hardware

| Componente                        | Cantidad | Notas                                        |
| --------------------------------- | :------: | -------------------------------------------- |
| Placa de desarrollo ESP32         |    1     | Modelo ESP32 DevKitC o similar               |
| Módulo de potencia del termo      |    1     | Para controlar las resistencias              |
| Sensores de temperatura DS18B20   |    2     | Modelo sumergible                            |
| Pantalla OLED 1.3" I2C            |    1     | Modelo SH1106 (128x64)                       |
| Pulsadores                        |    3     | Para el control manual                       |
| Zumbador Pasivo                   |    1     | Para feedback sonoro                         |
| Fuente de alimentación 220V a 5V  |    1     | Por ejemplo, un HLK-PM01 o similar           |
| Resistencias, cables, etc.        |  Varios  | Material auxiliar para las conexiones        |
| Placa del display y botones       | Opcional | Usando la propia del termo, modificada       |

---

## 🔌 Wiring y Esquemas

### Pinout del ESP32

La siguiente tabla detalla las conexiones entre los pines del ESP32 y los diferentes componentes del sistema.

| Pin ESP32 | GPIO   | Componente Conectado                      |
| --------- | ------ | ----------------------------------------- |
| `PinRele1`  | `GPIO22` | Relé Resistencia Tanque 1                 |
| `PinRele2`  | `GPIO21` | Relé Resistencia Tanque 2                 |
| `PinRele3`  | `GPIO19` | Relé Resistencia Modo TURBO               |
| `PinDallas` | `GPIO4`  | Bus OneWire para sensores DS18B20         |
| `PinBtnOnOff`| `GPIO25` | Pulsador ON/OFF                           |
| `PinBtnMode`| `GPIO33` | Pulsador de Cambio de Modo                |
| `PinBtnTmp` | `GPIO32` | Pulsador de Ajuste de Temperatura         |
| `PinLed1`   | `GPIO14` | LED Indicador Tanque 1 Activo             |
| `PinLed2`   | `GPIO26` | LED Indicador Tanque 2 Activo             |
| `PinLedTurbo`|`GPIO27` | LED Indicador Modo TURBO Activo           |
| `PinI2C_SCL`| `GPIO23` | Pin SCL del bus I2C (Pantalla OLED)       |
| `PinI2C_SDA`| `GPIO18` | Pin SDA del bus I2C (Pantalla OLED)       |
| `PinBuzzer` | `GPIO16` | Salida para el Zumbador                   |

### 📸 Fotografías del Montaje

**(Imagen del esquema de cableado)**
`[Imagen del esquema de cableado]`

**(Imagen de la placa PCB del Display)**
`[Imagen de la placa PCB]`

**(Imagen del montaje final dentro del termo)**
`[Imagen del montaje final]`

---

## ⚙️ Software y Configuración

### Prerrequisitos

1.  Una instancia de **Home Assistant** en funcionamiento.
2.  El Add-on **ESPHome** instalado en Home Assistant.
3.  Los archivos de fuentes `arial.ttf` y `materialdesignicons-webfont.ttf`. Debes crear una carpeta llamada `fonts` dentro de tu directorio de configuración de ESPHome (`/config/esphome/fonts/`) y colocar los archivos allí.

### Código ESPHome

El corazón del proyecto es el archivo de configuración YAML. Puedes encontrar el código completo en el siguiente enlace. Se recomienda revisar el bloque `substitutions` en el fichero para adaptarlo a tus pines y configuración de red.

➡️ **[Ver el código: termo_control_esphome.yaml](ESPhome%20Code/V1%20termo_control_esphome.yaml)**

**¡Importante!** No olvides crear un archivo `secrets.yaml` en tu directorio de ESPHome para guardar tus credenciales de WiFi (`wifi_ssid`, `wifi_password`, etc.) y la clave de encriptación de la API (`ota_password`) de forma segura.

---

## 🏠 Integración con Home Assistant

Una vez que compiles y subas este código a tu ESP32, Home Assistant lo detectará automáticamente. Al añadirlo, se crearán las siguientes entidades para un control total desde tu panel de control.

<img   
  src="https://github.com/JesusHCU/Wesen-FLAT-ESPHome/blob/main/Images/Termo%20Inox%20%E2%80%93%20Home%20Assistant.jpg" 
  alt="Panel de Control en Home Assistant" 
  width="20%" height="auto">

### Entidades Creadas

-   **`select.termoinox_on_off`**: Selector para encender o apagar el termo.
-   **`select.termoinox_power_modo`**: Selector para elegir el modo de calentamiento (Tanque 1, Tanque 1+2, Turbo).
-   **`number.termoinox_objetivo_t1`**: Control numérico para ajustar la temperatura objetivo del Tanque 1.
-   **`number.termoinox_objetivo_t2`**: Control numérico para ajustar la temperatura objetivo del Tanque 2.
-   **`sensor.termoinox_tempt1`**: Temperatura actual del Tanque 1.
-   **`sensor.termoinox_tempt2`**: Temperatura actual del Tanque 2.
-   **`sensor.termoinox_senal_wifi`**: Intensidad de la señal WiFi del dispositivo.
-   ... y varios `switch` para control manual de relés y LEDs si se desea.

---

## 👨‍💻 Uso y Funcionamiento

### Control Físico

-   **Botón 1 (ON/OFF)**: Una pulsación enciende o apaga el sistema por completo. Si la pantalla está apagada, la primera pulsación la activará.
-   **Botón 2 (Modo)**: Con el sistema encendido, cada pulsación cicla entre los modos de calentamiento: `TANQUE 1` -> `TANQUE 1 + 2` -> `TANQUE 1 + 2 + TURBO`.
-   **Botón 3 (Temperatura)**:
    -   Si está en modo `TANQUE 1`, cada pulsación aumenta la temperatura objetivo del **Tanque 1** en 5°C.
    -   En los otros modos (`TANQUE 1 + 2` o `TURBO`), aumenta la temperatura objetivo del **Tanque 2** en 5°C.
    -   Al llegar a la temperatura máxima, vuelve a la mínima.

### Lógica de Calentamiento

-   El sistema tiene una **histéresis de 1.0°C**. Esto significa que las resistencias se activarán cuando la temperatura baje 1 grado por debajo del objetivo y se apagarán al alcanzarlo, evitando ciclos constantes de encendido y apagado.
-   El modo **TURBO** es un refuerzo para el Tanque 1; solo se activa si el relé del Tanque 1 ya está calentando.

---

## 👨‍💻 Autor

Este proyecto ha sido íntegramente desarrollado y es mantenido por **JesusHCU**.
