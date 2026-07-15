# 项目开发计划文档

## 基于 STM32 + FreeRTOS + CAN + Embedded Linux 的智能边缘控制终端系统


---

# 1. 开发目标


本项目计划在暑假期间完成一个完整的嵌入式系统开发。


最终实现：


- STM32实时控制节点
- FreeRTOS多任务系统
- CAN通信协议
- Embedded Linux边缘节点
- MQTT网络通信
- Web设备管理


形成完整系统闭环：
传感器

|

STM32

|

CAN

|

Linux

|

MQTT

|

用户端
---

# 2. 总体开发周期


预计开发周期：

## 40天


分为五个阶段：


|阶段|时间|目标|
|-|-|-|
|阶段1|Day1-Day7|STM32基础开发|
|阶段2|Day8-Day15|FreeRTOS系统开发|
|阶段3|Day16-Day25|CAN通信开发|
|阶段4|Day26-Day35|Linux节点开发|
|阶段5|Day36-Day40|系统联调优化|



---

# 3. Phase 1

# STM32基础开发

## Day 1-Day 7


目标：

熟悉STM32开发环境，并完成基础外设驱动。


---

## 学习内容


### 开发环境


- STM32CubeMX
- Keil / VS Code
- ST-Link


---

### STM32基础


掌握：

- GPIO
- UART
- Timer
- PWM
- ADC


---

### 通信接口


学习：

- I2C
- SPI


---

## 实现功能


完成：


### LED控制


实现GPIO输出。


---

### 串口调试


实现：

STM32 -> PC

数据输出。


---

### 传感器读取


完成：

MPU6050

DHT22


数据采集。



---

## 阶段成果


Git提交：
stm32_basic_driver



---

# 4. Phase 2

# FreeRTOS实时系统开发


## Day 8-Day 15


目标：

将传统裸机程序升级为实时操作系统。


---

## 学习内容


FreeRTOS核心概念：

- Task
- Queue
- Semaphore
- Mutex
- Timer


---

## 系统任务设计


实现：
Sensor Task

CAN Task

Control Task

Monitor Task

Debug Task



---

## 功能实现


完成：


### 多任务调度


传感器采集任务独立运行。


---

### 任务通信


使用：

Queue

实现数据传递。


---

### 系统监控


加入：

WatchDog


---

## 阶段成果


Git提交：



stm32_freertos_system



---

# 5. Phase 3

# CAN通信开发


## Day16-Day25


目标：

实现STM32与Linux之间的数据通信。


---

## 学习内容


CAN基础：

- CAN协议
- 数据帧
- 仲裁机制
- 波特率配置


---

## 硬件连接


完成：



STM32

|

CAN

|

Linux



---

## 软件实现


开发：


### CAN Driver


负责：

底层收发。


---

### CAN Protocol


设计：

自定义通信协议。


例如：



CMD_PWM_SET

TEMP_DATA

DEVICE_STATUS



---

## 测试


实现：

STM32发送数据

Linux接收数据。


---

## 阶段成果


Git提交：



can_communication_module



---

# 6. Phase 4

# Embedded Linux节点开发


## Day26-Day35


目标：

完成Linux边缘计算节点。


---

## 学习内容


Linux开发：


- Shell
- GCC
- C/C++
- CMake
- Socket


---

## Linux功能开发


实现：


## CAN数据接收


完成：

Linux读取CAN数据。


---

## 数据解析


实现：

协议解析模块。


---

## 数据存储


加入：

SQLite


保存：

设备状态。


---

## 网络通信


实现：

MQTT Client


数据上传服务器。


---

## Web管理


实现简单接口：


功能：

- 查看状态
- 控制设备


---

## 阶段成果


Git提交：



linux_gateway_system



---

# 7. Phase 5

# 系统联调与优化


## Day36-Day40


目标：

完成最终Demo。


---

## 联调内容


### 数据链路测试


完整流程：



Sensor

↓

STM32

↓

CAN

↓

Linux

↓

MQTT

↓

Web



---

## 性能优化


优化：

- 任务优先级
- 通信稳定性
- 内存使用


---

## 文档完善


完成：

- README
- 使用说明
- 系统截图
- 测试报告


---

# 8. 最终项目成果


最终仓库结构：



STM32-Linux-Edge-Control-System

├── docs

│ ├── project_design.md

│ ├── hardware_design.md

│ ├── software_arch.md

│ └── development_plan.md

├── stm32_firmware

│ └── STM32代码

├── linux_gateway

│ └── Linux程序

├── server

│ └── Web服务

└── README.md



---

# 9. Git开发规范


项目开发过程中保持：


## 每完成一个功能


提交一次：


例如：



git add .

git commit -m "Implement CAN communication module"

git push




---

# 10. 最终展示目标


项目Demo：


用户通过Web发送控制指令。


流程：



Web

↓

Linux Gateway

↓

CAN

↓

STM32

↓

PWM控制设备



同时：

Linux显示：

- 设备状态
- 传感器数据
- 通信状态


---

# 11. 项目能力总结


通过该项目掌握：


## MCU开发

- STM32
- C语言
- 外设驱动


## 实时系统

- FreeRTOS


## 工业通信

- CAN


## Linux开发

- ARM Linux
- C/C++


## 网络通信

- MQTT
- TCP/IP


最终形成：

一个完整的嵌入式智能边缘控制系统开发能力。
