# 软件架构设计文档

## 基于 STM32 + FreeRTOS + CAN + Embedded Linux 的智能边缘控制终端系统

---

# 1. 软件架构概述


本项目采用分层式软件架构设计。


整体软件系统由三个部分组成：

1. STM32实时控制系统

2. Embedded Linux边缘计算系统

3. 上层网络管理系统


系统通过CAN通信连接STM32和Linux，实现实时控制与复杂计算任务分离。



整体软件架构：
             Web管理端

                 |

              HTTP/MQTT

                 |

    --------------------------------

          Embedded Linux

    --------------------------------

    Application Layer

    Communication Layer

    Data Processing Layer


                 |

              CAN Bus


                 |

    --------------------------------

             STM32

    --------------------------------


    Application Layer

    RTOS Layer

    Driver Layer

    Hardware Layer


---

# 2. 软件设计原则


## 2.1 模块化设计


系统按照功能进行模块划分：

- 驱动模块
- 通信模块
- 任务模块
- 数据处理模块


降低模块之间耦合度，提高可维护性。


---

## 2.2 实时性设计


STM32负责实时任务：

例如：

- 数据采集
- PWM控制
- 状态监测


Linux负责非实时任务：

例如：

- 数据存储
- 网络通信
- 用户交互


通过双处理器架构保证系统实时性。


---

# 3. STM32软件架构设计


STM32采用：

C语言 + FreeRTOS


软件结构：
stm32_firmware

├── BSP

│ ├── uart

│ ├── can

│ ├── i2c

│ ├── spi

├── Drivers

├── FreeRTOS

├── Application

│

├── sensor_task.c

├── can_task.c

├── control_task.c

├── monitor_task.c

└── main.c


---

# 4. STM32分层设计


## 4.1 Hardware Layer


负责：

- STM32芯片
- GPIO
- UART
- SPI
- I2C
- CAN


提供底层硬件访问。


---

## 4.2 Driver Layer

负责：
外设驱动封装。
例如：mpu6050.c
dht22.c
oled.c
can_driver.c


应用层无需关注硬件细节。


---

## 4.3 RTOS Layer


采用：

FreeRTOS


负责：

- 任务调度
- 资源管理
- 任务通信



使用：

- Task
- Queue
- Semaphore
- Mutex



---

## 4.4 Application Layer


实现设备业务逻辑。


包括：


### Sensor Task


功能：

周期采集传感器数据。


流程：ensor

↓

Read Data

↓

Queue

↓

Control Task



---

### CAN Task


功能：

负责CAN通信。


接收：

Linux控制指令


发送：

设备状态数据



---

### Control Task


功能：

执行控制逻辑。


例如：

根据温度控制PWM输出。



---

### Monitor Task


功能：

系统状态监测。


检测：

- 传感器异常
- 通信异常
- 参数异常



---

# 5. FreeRTOS任务设计


系统任务划分：


|任务|优先级|功能|
|-|-|-|
|Control Task|High|实时控制|
|CAN Task|High|通信处理|
|Sensor Task|Medium|数据采集|
|Monitor Task|Medium|状态检测|
|Debug Task|Low|日志输出|


---

任务通信方式：
Sensor Task

  |

Queue

  |

Control Task


共享资源：

使用：

Mutex


避免：

资源竞争。


---

# 6. CAN通信软件设计


CAN通信采用：

分层设计。
CAN Driver

 |

CAN Protocol

 |

Application



---

# 6.1 CAN协议设计


消息格式：


|字段|说明|
|-|-|
|ID|消息类型|
|DLC|数据长度|
|DATA|数据内容|



---

# 6.2 通信方向


## Linux -> STM32


控制命令：
CMD_START

CMD_STOP

CMD_PWM_SET

CMD_RESET



---

## STM32 -> Linux


状态数据：



TEMP_DATA

DEVICE_STATUS

ERROR_INFO


---

# 7. Embedded Linux软件架构


Linux端采用：

C/C++开发。


软件结构：
linux_gateway

├── can

│ └── can_manager.cpp

├── protocol

│ └── parser.cpp

├── mqtt

│ └── mqtt_client.cpp

├── database

│ └── sqlite.cpp

├── device

│ └── device_manager.cpp

└── main.cpp


---

# 8. Linux模块设计


## 8.1 CAN通信模块


功能：

- 接收CAN数据
- 数据解析
- 转换为系统消息



---

## 8.2 数据管理模块


负责：

- 数据缓存
- 状态管理
- 历史记录


存储：

SQLite


---

## 8.3 MQTT通信模块


负责：

设备与服务器通信。


数据流程：
STM32

↓

CAN

↓

Linux

↓

MQTT

↓

Server


---

# 9. 数据流设计


完整数据流程：
传感器

|

STM32 Driver

|

Sensor Task

|

CAN Protocol

|

CAN Bus

|

Linux CAN Manager

|

Data Processing

|

MQTT/Web


---

# 10. 异常处理设计


系统支持异常检测。


包括：


## 通信异常


例如：

CAN超时


处理：

重新连接。


---

## 传感器异常


例如：

数据异常


处理：

报警。


---

## 系统异常


例如：

任务阻塞


处理：

WatchDog复位。



---

# 11. 后续扩展设计


## 多节点CAN网络


支持：

多个STM32节点。
STM32 Node1

   |

  CAN

   |

STM32 Node2

   |

  CAN

   |

Linux Gateway


---

## AI能力扩展


Linux节点未来支持：

- AI推理
- 智能决策
- Agent控制


形成：
AI Agent

|

Linux

|

STM32

|

Physical Device


---

# 12. 总结


本项目采用：

STM32 + FreeRTOS + Embedded Linux

双处理器软件架构。


通过：

- RTOS实时任务管理
- CAN工业通信
- Linux边缘计算
- 网络服务


实现一个完整的智能嵌入式控制系统。


该架构具有：

实时性

可靠性

扩展性

符合工业物联网设备的软件设计思想。


