# STM32 四轴飞行器微型飞控硬件系统 (4-Layer PCB)

本项目为一套高集成度、微型四轴飞行器飞控硬件系统，全板基于 Altium Designer 完成四层高密度 PCB 设计与投产打样，并通过 LTspice 进行了电机驱动瞬态反冲电压抑制仿真验证。

## 核心硬件架构与指标
- **主控平台**：STM32F103T8U6 (QFN-36 紧凑封装，72MHz 主频)
- **姿态传感**：MPU6050 六轴传感器，就近配置 LC 低通滤波网络与参考地隔离
- **无线通信**：GC2400-TC017 2.4GHz 高速无线射频模组 (SPI 驱动)
- **动力拓扑**：FP6276BXR-G1 异步 Boost 升压（1S 锂电升压至 5V 动力轨）+ TP2019-3.3 超低噪声 LDO 二次降压
- **驱动拓扑**：4 路 CJ2310 N-MOSFET 驱动 716 空心杯电机，并联 1N5819W 肖特基续流二极管抑制高频反冲电压尖峰

## 四层板信号与电源完整性 (SI/PI)
1. **叠层规划**：L1(Top 信号) - L2(GND 连续地平面) - L3(Power 电源平面) - L4(Bottom 辅助走线与散热地)。
2. **抗干扰设计**：动力回路最短化，高灵敏传感器模拟区与大电流动力区实现单点接地，规避地弹干扰。
3. **瞬态仿真**：提供 `Motor_Drive_Simulation.asc`，验证了 PWM 关断瞬态下的电压钳位效果，防止 MOSFET 击穿。

## 仓库文件清单
- `Quadcopter_FC_Hardware_Portfolio_FINAL_V2.1.pdf`：12 页全流程工程作品集。
- `Gerber.zip`：标准化制造光绘与 NC 钻孔文件。
- `BOM.xlsx` & `Pick Place for Quadcopter_FC.csv`：生产物料清单与 SMT 贴装坐标。
- `Source_Altium/`：完整 Altium Designer 工程源码（PrjPcb / PcbDoc / SchDoc）。
