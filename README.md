# Sistema de Medición de Tiempo para Movimiento Mecánico

![image](https://github.com/user-attachments/assets/e328f309-7885-4ee9-ad4e-5c24fae3ee16)

![Recording 2025-04-05 at 11 09 05](https://github.com/user-attachments/assets/ed5c8633-f124-41c9-812e-ae3c39e33899)

Sistema embebido para analizar el movimiento angular de una barra rígida acoplada a un motor paso a paso, implementando sensores ópticos y acelerómetro para medición precisa.

## 📌 Objetivos

### Objetivo General
Desarrollar un sistema de medición de tiempo para analizar el movimiento de una barra rígida desde 0° hasta 90° utilizando:
- Temporizador STM32
- Acelerómetro MPU6050
- Sensores ópticos CNY70
- GPIO digital

### Objetivos Específicos
1. Control preciso de motor paso a paso 28BYJ-48 con microstepping
2. Medición angular con acelerómetro/giroscopio MPU6050
3. Delimitación de rango 0°-90° con sensores ópticos CNY70
4. Interfaz de control con botones físicos

## 🛠 Hardware Utilizado
| Componente | Especificaciones |
|------------|------------------|
| Microcontrolador | STM32F411RET6 |
| Motor Paso a Paso | 28BYJ-48 + Driver ARD-300 |
| Sensores Ópticos | 2x CNY70 |
| Acelerómetro | MPU6050 (6 ejes) |
| Periféricos | 3 botones, resistencias 220Ω/10kΩ |

## 📋 Configuración

### Diagrama de Conexiones
![image](https://github.com/user-attachments/assets/a62b4654-b644-4c03-b716-319b945ed7a6)



### Pines STM32
| Función | Pin | Configuración |
|---------|-----|---------------|
| Fases Motor | F0-F3 | Salida PWM |
| Sensores CNY70 | PA0-PA1 | Entrada digital |
| Botones | PC0-PC2 | Entrada pull-up |
| I2C (MPU6050) | PB6-PB7 | SDA/SCL |

## ⚙️ Funcionamiento

### Flujo Principal
1. Inicio con botón 1 (PC0)
2. Motor gira hasta 90° (detectado por CNY70)
3. MPU6050 registra ángulo en tiempo real
4. Timer mide duración del movimiento
5. Datos enviados por UART (115200 bauds)

## ⚙️ Configuración Minicom

# MacOS (Homebrew)
- brew install minicom
- ls /dev/cu.*
- minicom -D /dev/tty.usbmodem1112203 -b 115200

![image](https://github.com/user-attachments/assets/dac0bf5f-17c0-4c7a-afdd-6fe893394b40)


# Modo SUDO para abrir STM32CUBEIDE
sudo "/Applications/STM32CubeIDE.app/Contents/MacOS/STM32CubeIDE"


**Referencia:**

- **Título del repositorio**: STM32-Tutorials  
- **Autor**: MYaqoobEmbedded  
- **Tutorial específico**: Tutorial 35 - MPU 6050 IMU Module  
- **URL del repositorio**: [https://github.com/MYaqoobEmbedded/STM32-Tutorials](https://github.com/MYaqoobEmbedded/STM32-Tutorials)  
- **URL específica del tutorial**: [https://github.com/MYaqoobEmbedded/STM32-Tutorials/tree/master/Tutorial%2035%20-%20MPU6050%20IMU%20Module](https://github.com/MYaqoobEmbedded/STM32-Tutorials/tree/master/Tutorial%2035%20-%20MPU6050%20IMU%20Module)  

**Nota:** Aunque utilizamos la librería del repositorio para el sensor MPU6050 como base, el desarrollo de nuestra práctica integradora se apoyó en un archivo `main.c` adaptado con funcionalidades adicionales desarrolladas por el Dr. Víctor Hugo Benítez, así como en otros recursos y prácticas realizadas en las calses de sistemas embebidos.






