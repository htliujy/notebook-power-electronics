# Power-Electronics

这个blog是用来做电力电子相关技术的分享，记录这些知识，可以增强自己的理解，加强记忆，同时用于分享给他人促进交流。

内容分类：

- 功率器件：包括功率开关管，功率二级管，功率磁性器件，功率阻容器件
- 电源拓扑
- 效率
- 环路
- EMC
- 测试及可靠性
- 等等

待写清单：

- MOS SOA
- IGBT 驱动 负压驱动
- 死区时间
- MOS 并联稳定性
- 开关电源软启动
- 安规（看起来要独立成一章）
- DSP 加密方式
- callback 函数
- LPR 校验
- CRC 校验
- TEA 加密
- 电子伏特和波长频率（可见光的电子伏特数量）（要是能写一个计算器，用于计算对应的电子伏特就好了，虽然网上就有，那就用python写一个吧！）
- Mac使用技巧：如何更新截图默认存储路径
- 开关电源，同步整流MOS为什么放在下端，不放在上端，其实二极管放在哪端都行，只是放在下端，变压器的下端不接地，看起来怪怪的。
- 开关管是否能做到真正的对称？电子迁移率和空穴迁移率不一样。
- 化学材料测试：撕裂的Propagation
- MOS 管电流饱和，是因为沟道夹断还是电子迁移率达到了最大值？
- FOM (Figure of Merit)如何判定半导体的优劣？
- MOS datasheet解读。
- 反激拓扑设计，[零基础带你了解反激变换器](https://www.eefocus.com/analog-power/469103)
- 疑问：IGBT什么是饱和区？《基于有源门极驱动的IGBT串联均压技术研究》
  - 变流器在运行时，由于负载工作的不确定性，IGBT过流时有发生。 IGBT正常导通时压降很小，因此通态损耗也很小。当 IGBT出现过流时 ，如果驱动电路没能及时处理，则流过 IGBT的电流可能持续上升，当流过 IGBT的电流超过一定程度（通常为额定电流的 3~4倍 IGBT将退出饱和区进入有源区， IGBT两端电压上升到系统直流电压。此时 IGBT将同时工作在高电压和大电流状态，损耗急剧上升，严重时会发生损坏。因此，在 IGBT发生过流时驱动电路需要及时地发现过流现象并关断 IGBT。 短路故障也是变流器常见的故障之一 IGBT发生短路时由于电流路径的阻抗很小 因此短路电流将在很短的时间内上升到额定电流的 3~4倍 使 IGBT退出饱和区 。 因此 驱动电路需要能够及时地发现短路故障并关断 IGBT 防止其瞬态功率超过极限值而损坏 。但是 IGBT在过流或短路状态下，由于电流很大，若采用传统的方法关断，电流下降速
- 高压直流输电
  - 并联

## 开关电源

### 开关电源基本拓扑

1. 线性电源与开关电源的定义
2. 开关电源三种基本拓扑（非隔离型）
   1. Buck
   2. Boost （具体应用：PFC电路）
   3. Buck-Boost

### 隔离型开关电源拓扑

1. 隔离的方法与必要性
2. 硬开关拓扑
   1. 反激电路
   2. 正激电路
   3. 推挽电路
3. 软开关拓扑
   1. LLC谐振电路
   2. QR反激电路
   3. 有源钳位反激电路

### 开关电源中的关键元器件

1. 储能元件
   1. 电容（相关公式以及各种类型的电容介绍）
   2. 电感（相关公式以及各种类型的电感介绍）
   3. 变压器
2. 二极管
   1. 常见二极管器件（PN二极管、肖特基二极管、快恢复二极管等）
   2. 整流二极管
   3. 续流二极管
3. 开关器件
   1. 常见开关器件（三极管，Si MOSFET、晶闸管、IGBT，GaN HEMT，SiC MOSFET等）
   2. 开关器件的关键参数
   3. 同步整流技术
4. 安规器件
   1. 隔离器件（变压器、光耦、隔离驱动）
   2. EMC器件（X电容、Y电容、共模电感、差模电感）
   3. 保护器件（热敏电阻、压敏电阻、保险丝）

### 开关电源中各元件损耗分析

   1. 开关器件损耗
   2. 二极管损耗
   3. 变压器损耗
   4. 其他元件损耗（电容、电感的ESR损耗等）
