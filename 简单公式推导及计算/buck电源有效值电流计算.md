---
title: buck电源有效值电流计算
date: 2020/05/16 12:35:46
categories: 技术杂谈
tags:
 - 开关电源
mathjax: true
---
# buck电源有效值电流计算

## buck 电路如下图：

![buck电路](./images/buck电源有效值电流计算/figure1_buck_current.png)

下面开始分析不同阶段的整流、续流电流有效值。
<!-- more -->

令$$\Delta I = I_p-I_v$$,也就是峰峰值，且假定上管开通的瞬间为0时刻，也是电流谷值$$I_v$$点，那么$$T_{on}$$阶段，有：
$$
{I=I_{out}-\frac{\Delta{I}}{2}+\frac{\Delta{I}}{T_{on}}t}
$$

所以有：

$$\begin{align}
I^2 & =I_{out}^2+(\frac{\Delta{I}}{2})^2+(\frac{\Delta{I}}{T_{on}})^2t^2-I_{out}\Delta{I}+\frac{2I_{out}\Delta{I}}{T_{on}}t-\frac{\Delta{I}^2}{T_{on}}t\\
\end{align}$$

对电流的平方进行积分，得到：
$$\begin{align}
\int_{0}^{Ton}I^2\mathrm{d}t& = \int_{0}^{Ton}\bigg[I_{out}^2+(\frac{\Delta{I}}{2})^2+(\frac{\Delta{I}}{T_{on}})^2t^2-I_{out}\Delta{I}+\frac{2I_{out}\Delta{I}}{T_{on}}t-\frac{\Delta{I}^2}{T_{on}}t\bigg]\mathrm{d}t\\
& = \int_{0}^{Ton} \bigg[I_{out}^2+(\frac{\Delta{I}}{2})^2-I_{out}\Delta{I}\bigg] \mathrm{d}t+\int_{0}^{Ton}\bigg[(\frac{\Delta{I}}{T_{on}})^2t^2+(\frac{2I_{out}\Delta{I}}{T_{on}}-\frac{\Delta{I}^2}{T_{on}})t\bigg]\mathrm{d}t\\
&=\bigg[I_{out}^2+(\frac{\Delta{I}}{2})^2-I_{out}\Delta{I}\bigg]T_{on}+\frac{1}{3}(\frac{\Delta{I}}{T_{on}})^2T_{on}^3+(\frac{I_{out}\Delta{I}}{T_{on}}-\frac{\Delta{I}^2}{2T_{on}})T_{on}^2\\
&=\bigg[I_{out}^2+(\frac{\Delta{I}}{2})^2-I_{out}\Delta{I}+\frac{1}{3}\Delta{I}^2+I_{out}\Delta{I}-\frac{1}{2}\Delta{I}^2\bigg]T_{on}\\
&= (I_{out}^2+\frac{1}{12}\Delta{I}^2)T_{on}
\end{align}$$

所以在$$T_{on}$$阶段(单纯这一小阶段，而不是整个开关周期)：
$$\begin{align}
I_{rms\_on}&=\sqrt{\frac{\int_{0}^{Ton}I^2\mathrm{d}t}{T_{on}}}\\
&=\sqrt{I_{out}^2+\frac{1}{12}\Delta{I}^2}
\end{align}$$

输入开关管(上管)的电流有效值为（在一整个开关周期$$T_S$$内的有效值电流）：
$$\begin{align}
I_{rms\_up}&=\sqrt{\frac{\int_{0}^{Ton}I^2\mathrm{d}t}{T_s}}\\
&=\sqrt{(I_{out}^2+\frac{1}{12}\Delta{I}^2)D}
\end{align}$$

同理，在$$T_{off}$$内：
$$\int_{0}^{Toff}I^2\mathrm{d}t=(I_{out}^2+\frac{1}{12}\Delta{I}^2)T_{off}$$

所以在$$T_{off}$$阶段(单纯这一小阶段，而不是整个开关周期)：
$$\begin{align}
I_{rms\_off}&=\sqrt{\frac{\int_{0}^{Toff}I^2\mathrm{d}t}{T_{off}}}\\
&=\sqrt{I_{out}^2+\frac{1}{12}\Delta{I}^2}
\end{align}$$

下管电流有效值（在一整个开关周期$$T_{S}$$内的有效值电流）：
$$\begin{align}
I_{rms\_dowm}&=\sqrt{\frac{\int_{0}^{Toff}I^2\mathrm{d}t}{T_s}}\\
&=\sqrt{(I_{out}^2+\frac{1}{12}\Delta{I}^2)(1-D)}
\end{align}$$

输出电感电流有效值，就是整个开关周期内的输出电流有效值：
$$\begin{align}
I_{rms}&=\sqrt{\frac{\int_{0}^{Ton}I^2\mathrm{d}t+\int_{0}^{Toff}I^2\mathrm{d}t}{T_s}}\\
&=\sqrt{I_{out}^2+\frac{1}{12}\Delta{I}^2}
\end{align}$$

## The END
