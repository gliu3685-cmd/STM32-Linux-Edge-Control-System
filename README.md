# STM32 Linux Edge Control System

## 基于 STM32 + FreeRTOS + CAN + Embedded Linux 的智能边缘控制终端系统


<p align="center">

An Industrial IoT-oriented embedded edge control system based on dual-processor architecture.

</p>


---

# 1. 项目简介


本项目设计并实现一个面向工业物联网场景的智能边缘控制终端。


系统采用：

**STM32 + Embedded Linux 双处理器架构**


其中：

- STM32负责实时控制、数据采集以及设备驱动
- Embedded Linux负责数据处理、网络通信以及设备管理


通过CAN总线实现两个处理器之间的可靠通信。


最终实现：
传感器采集

    ↓

STM32实时控制

    ↓

CAN通信

    ↓

Linux边缘计算

    ↓

MQTT/Web管理



---

# 2. 项目特点


## 2.1 双处理器协同架构


采用：


Linux
|
CAN
|
STM32



实现：

- 实时控制
- 边缘计算
- 网络通信


---

## 2.2 FreeRTOS实时系统


STM32端采用FreeRTOS。


任务划分：

- Sensor Task
- CAN Task
- Control Task
- Monitor Task
- Debug Task


实现多任务调度和模块解耦。


---

## 2.3 工业通信设计


采用：

CAN Bus


实现：

- 控制指令下发
- 设备状态上传
- 错误信息反馈


---

## 2.4 完整系统闭环


系统覆盖：


Hardware

↓

Driver

↓

RTOS

↓

Communication

↓

Linux Application

↓

Network Service



---

# 3. 系统架构


             User

              |

          Web Interface

              |

          MQTT / HTTP

              |

    ----------------------

      Embedded Linux

    ----------------------

      Data Processing

      Network Service

      Device Manager


              |

            CAN Bus


              |

    ----------------------

          STM32

    ----------------------

      FreeRTOS

      Drivers

      Control Logic


              |

      Sensors / Actuators


---

# 4. 技术栈


## MCU

- STM32F407
- ARM Cortex-M4
- C Language


## Real-Time System

- FreeRTOS


## Communication

- CAN
- UART
- SPI
- I2C


## Embedded Linux

- ARM Linux
- C/C++
- CMake


## Network

- MQTT
- TCP/IP


## Backend

- Python
- FastAPI
- SQLite



---

# 5. 硬件组成


|模块|设备|
|-|-|
|MCU|STM32F407|
|Linux节点|Orange Pi / ARM Linux Board|
|通信|CAN Bus|
|传感器|MPU6050、DHT22|
|显示|OLED|
|执行器|PWM/GPIO控制模块|


---

# 6. 项目目录结构



STM32-Linux-Edge-Control-System

├── README.md

├── docs

│ ├── project_design.md

│ ├── hardware_design.md

│ ├── software_arch.md

│ └── development_plan.md

├── stm32_firmware

│ └── STM32 Firmware

├── linux_gateway

│ └── Embedded Linux Application

└── server

└── Web Management Service


---

# 7. 开发计划


当前阶段：

## Phase 0: Project Design

完成：

- 系统需求分析
- 硬件方案设计
- 软件架构设计
- 开发路线规划


---

后续计划：


|阶段|内容|
|-|-|
|Phase 1|STM32基础开发|
|Phase 2|FreeRTOS系统开发|
|Phase 3|CAN通信实现|
|Phase 4|Linux Gateway开发|
|Phase 5|系统联调与优化|


详细计划：

[Development Plan](docs/development_plan.md)


---

# 8. 文档索引


## 项目设计

[Project Design](docs/project_design.md)


## 硬件设计

[Hardware Design](docs/hardware_design.md)


## 软件架构

[Software Architecture](docs/software_arch.md)


## 开发计划

[Development Plan](docs/development_plan.md)



---

# 9. 项目目标


通过本项目学习并实践：


- 嵌入式系统设计
- STM32 MCU开发
- FreeRTOS实时系统
- CAN工业通信
- Embedded Linux开发
- IoT边缘计算


最终实现一个具有：

- 实时性
- 可靠性
- 扩展性


的智能边缘控制终端。


---

# 10. License


This project is for learning and research purposes.
