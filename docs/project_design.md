# 基于 STM32 + FreeRTOS + CAN + Embedded Linux 的智能边缘控制终端系统

## Project Design Document

---

# 1. 项目简介

## 1.1 项目名称

基于 STM32 + FreeRTOS + CAN + Embedded Linux 的智能边缘控制终端系统

英文：

Intelligent Edge Control Terminal Based on STM32, FreeRTOS and Embedded Linux


---

## 1.2 项目背景

随着工业自动化和物联网技术的发展，传统设备逐渐向智能化、网络化方向发展。

工业现场通常需要：

- 实时采集设备状态
- 高可靠通信
- 本地实时控制
- 远程数据管理

单一处理器往往难以同时满足实时控制和复杂计算需求。

因此，本项目设计一种双处理器协同架构：

- STM32负责实时控制任务
- Embedded Linux负责数据处理和网络通信

实现一个具有工业物联网特征的智能边缘控制终端。


---

# 2. 项目目标

本项目目标是设计并实现一个完整的嵌入式控制系统，实现：

1. 传感器数据采集

2. 实时控制任务管理

3. CAN总线通信

4. Linux边缘计算节点

5. 网络数据传输

6. 远程设备控制

最终形成一个具备：

- 数据采集
- 数据处理
- 通信
- 控制

能力的嵌入式系统。


---

# 3. 系统总体架构
            用户端

          Web管理平台

                |

             MQTT/HTTP

                |

    ----------------------------

         Embedded Linux

      (边缘计算节点)

    ----------------------------

                |

             CAN Bus

                |

    ----------------------------

          STM32 Controller

    ----------------------------

      |          |           |

   Sensor     Control     Status

 传感器       执行器      状态监测


---

# 4. 系统功能设计


## 4.1 STM32实时控制模块


STM32作为底层控制核心，负责：

- 外设驱动
- 实时任务调度
- 数据采集
- 执行控制


主要功能：

### (1) 传感器采集

支持：

- 温湿度传感器
- IMU传感器


通信接口：

- I2C
- SPI


---

### (2) 执行控制


支持：

- PWM控制
- GPIO控制


例如：

- 风扇调速
- LED控制
- 继电器控制


---

### (3) 状态管理


实现：

- 设备状态检测
- 异常报警
- 通信状态监测



---

# 5. FreeRTOS实时系统设计


采用FreeRTOS实现多任务管理。


任务划分：


## Sensor Task

功能：

周期读取传感器数据。


## CAN Task

功能：

负责CAN通信。


## Control Task

功能：

执行控制逻辑。


## Monitor Task

功能：

设备状态检测。


## Debug Task

功能：

输出系统日志。



任务之间通过：

- Queue
- Semaphore
- Mutex

进行通信。



---

# 6. CAN通信设计


CAN作为STM32与Linux之间的数据通信协议。


通信方向：

Linux

|

CAN

|

STM32



设计自定义CAN协议。


数据格式：

|字段|说明|
|-|-|
|ID|消息类型|
|DATA|数据内容|
|CRC|校验信息|



支持：


Linux -> STM32:

- 控制命令
- 参数配置


STM32 -> Linux:

- 传感器数据
- 状态信息
- 错误信息



---

# 7. Embedded Linux模块


Linux作为系统边缘节点。


主要功能：

## 7.1 CAN数据处理


负责：

- 接收CAN数据
- 数据解析
- 状态管理


开发语言：

C/C++


---

## 7.2 网络通信


支持：

MQTT协议


实现：

设备数据上传。


---

## 7.3 数据存储


采用：

SQLite


保存：

- 历史数据
- 设备状态


---

# 8. Web管理模块


提供简单设备管理界面。


功能：

## 数据展示

显示：

- 温度
- 湿度
- 设备状态


## 设备控制

支持：

- 开启设备
- 修改参数



---

# 9. 技术栈


## MCU

- STM32F407
- ARM Cortex-M4


## Embedded System

- FreeRTOS


## Communication

- CAN
- UART
- SPI
- I2C


## Linux

- Embedded Linux
- C/C++


## Network

- MQTT
- TCP/IP


## Backend

- Python
- FastAPI
- SQLite



---

# 10. 项目特色


相比传统STM32项目，本项目特点：

## 1. 双处理器架构

STM32 + Linux协同工作。


## 2. 实时操作系统

使用FreeRTOS进行任务管理。


## 3. 工业通信协议

采用CAN总线。


## 4. 完整系统闭环

覆盖：

硬件

↓

底层驱动

↓

实时系统

↓

通信

↓

网络服务

↓

用户控制



---

# 11. 开发计划


## Phase 1

STM32基础开发

目标：

完成外设驱动。


## Phase 2

FreeRTOS系统设计


目标：

完成多任务系统。


## Phase 3

CAN通信实现


目标：

STM32与Linux通信。


## Phase 4

Linux节点开发


目标：

完成数据处理和网络通信。


## Phase 5

系统联调


目标：

完成完整Demo。



---

# 12. 项目最终目标


完成一个具有：

- 实时控制能力
- 网络通信能力
- 边缘计算能力

的智能嵌入式控制终端。


用于探索：

- 工业物联网
- 智能设备
- 边缘计算

方向。

