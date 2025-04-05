# Sistema de Medición de Tiempo para Movimiento Mecánico

![Diagrama de Hardware](https://via.placeholder.com/400x200?text=Ensamblado+Físico+del+Sistema)

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
![Esquema de conexiones](https://via.placeholder.com/600x400?text=Diagrama+de+Conexiones)

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

```c
// Ejemplo de lectura MPU6050
MPU6050_Get_Accel_Scale(&myAccelScaled);
ANG[0] = atan(myAccelScaled.x/sqrt(pow(myAccelScaled.y,2)+pow(myAccelScaled.z,2))) * RAD_Deg;
