# MOSFET-datasheet解读

1. 雪崩（温度系数），需要测试数据图片。
2. Ron（温度系数）。
3. Normalized 归一化参数
4. IV的SOA和温升-时间曲线
5. MOS的特性

## 最大电流

功率MOSFET中，一般会标明两种最大电流：持续最大电流（直流）和脉冲最大电流。他们分别是如何限定的？

### 最大持续 DS 电流

IRFP3206PbF的规格书对于最大持续电流的限定，如下图<sup>[1]</sup>:

<div  align="center">
<img src="./MOSFET-datasheet解读/IRFP3206PbF_max_continuous_DS_current.png" width = "100%" height = "100%" alt="max_continuous_DS_current" align=center />
</div>

在外壳温度保持25℃的情况下，持续电流为**200A**，该电流数值是如何得到的？

其实很简单，是结温限定，也就是，在外壳温度为25℃时，使得结温为150℃的持续电流就是最大持续电流。

根据结温计算公式：

$$
\begin{aligned}
T_J = R_{\theta JC} \cdot P_D + T_C
\end{aligned}
$$

其中：

- $$T_J$$为结温
- $$R_{\theta JC}$$为 junction（半导体结） 到 case (封装外壳) 的热阻
- $$P_D$$为耗散功率功率，也就是MOS管导通损耗功率
- $$T_C$$为外壳温度

有：

$$
\begin{aligned}
P_D = I_{DS}^2 \cdot R_{DS(on)}
\end{aligned}
$$

其中:

- $$I_{DS}$$ 为MOS管的DS电流
- $$R_{DS(on)}$$ 为MOS管的导通电阻，此电阻与结温相关，若是MOS管的结温为150℃，那么需要按照150℃时的导通电阻计算MOS管的导通损耗

那么有：

$$
\begin{aligned}
I_{DS} =\sqrt {\frac{T_J - T_C}{R_{\theta JC} \cdot R_{DS(on)}}}
\end{aligned}
$$

参考IRFP3206PbF规格书，在25℃时，有 $$R_{DS(on)\_max} = 3.0m\Omega$$，那么根据$$R_{DS(on)}$$ 的温度系数曲线，可以得到$$R_{DS(on)}\_max\_150℃ = 1.91 \cdot 3.0m\Omega = 5.73m\Omega$$, 系数**1.91**为使用尺子直接在曲线上测量得到。

<div  align="center">
<img src="./MOSFET-datasheet解读/IRFP3206PbF_Ron温度系数曲线.png" width = "50%" height = "50%" alt="IRFP3206PbF_Ron温度系数曲线" align=center />
</div>

且，根据规格书中，$$R_{\theta JC}\_max = 0.54 ℃/W$$。得到：

$$
\begin{aligned}
I_{DS} &=\sqrt {\frac{\frac{T_J}{R_{\theta JC} } - T_C}{R_{DS(on)}}} \\
&= \sqrt {\frac{150℃ - 25℃}{0.54 ℃/W \cdot 5.73m\Omega }} \\
&= 200.99A
\end{aligned}
$$

与标称值200A相差0.5%，鉴于温度系数测量的不准确度（在图中曲线直接测量得到$$R_{DS(on)}$$的温度补偿1.91）大于1%，最终电流计算结果与datasheet标称值偏差0.5%这是合理的。

另外，可以参考以下器件的datasheet, 可以得到相同的结论。

- TPH3206PSB GaN FET datasheet
- IRFP3206PbF
- 24NM60

## 参考及引用

[1] IRFP3206PbF. datasheet. 3/3/08 <www.irf.com>
BSC017N04NS-datasheet
[2] STF13NM60N-datasheet
[3] IXBK55N300-datasheet(IGBT)
