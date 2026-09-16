# STM32 四轴飞行器飞控板 (4-Layer PCB)

基于开源四轴飞行器项目进行硬件方案设计，结合芯片数据手册重新设计飞控板硬件电路，完成原理图绘制、四层PCB设计及硬件调试。

## 我的工作

本人主要负责：

- 飞控板硬件方案设计与器件选型
- 基于芯片数据手册进行外围电路参数设计
- 原理图设计与25×50mm四层PCB设计
- 3.7V→5V→3.3V电源架构设计
- 4路MOSFET电机驱动电路设计
- PCB打样、焊接及硬件调试
- LTspice电机驱动瞬态仿真与电路优化

## 核心硬件架构

- **主控平台**：STM32F103T8U6，72MHz
- **姿态传感**：MPU6050 六轴传感器
- **无线通信**：GC2400-TC017 2.4GHz无线射频模组
- **电源架构**：FP6276BXR-G1 Boost DC-DC（1S锂电池升压至5V）+ TP2019-3.3 LDO（二次降压至3.3V）
- **电机驱动**：4路CJ2310 N-MOSFET驱动716空心杯电机
- **瞬态保护**：1N5819W肖特基续流二极管

## 四层PCB与SI/PI设计

1. **PCB叠层**：L1信号层 - L2连续GND平面 - L3电源层 - L4辅助走线与散热地。
2. **电源与回流设计**：L2采用连续GND平面，为高速及敏感信号提供连续低阻抗回流路径；L3对4路电机采用星型电源分配，减少公共供电路径上的压降及支路间干扰。
3. **射频设计**：GC2400-TC017板载天线区域进行全层铺铜挖空，降低PCB铜箔对2.4GHz射频性能的影响。
4. **瞬态仿真**：提供 `Motor_Drive_Simulation.asc`，通过LTspice分析PWM关断瞬态，加入1N5819W后将仿真中的约500V感应电压尖峰钳位至约4.45V。

## 仓库文件

- `Quadcopter_FC_Hardware_Portfolio_FINAL_V2.1.pdf`：12页硬件设计作品集
- `Gerber.zip`：PCB制造文件
- `BOM.xlsx`：物料清单
- `Pick Place for Quadcopter_FC.csv`：SMT贴装坐标文件
- `Motor_Drive_Simulation.asc`：LTspice电机驱动瞬态仿真
- `Source_Altium/`：Altium Designer工程源码
