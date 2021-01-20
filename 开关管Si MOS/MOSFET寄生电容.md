# MOSFET寄生电容

本文主要介绍MOSFET中，$$C_{oss}$$, $$C_{iss}$$, $$C_{rss}$$，以及他们和$$C_{gs}$$，$$C_{gd}$$，$$C_{ds}$$的关系。

如下图[1]：

<div  align="center">
<img src="./MOSFET寄生电容/MOSFET寄生电容.png" width = "100%" height = "100%" alt="MOSFET寄生电容" align=center />
</div>

图中的MOSFET是典型的功率MOSFET（垂直沟道）结构截面图。

$$C_{iss}$$：输入电容
$$C_{oss}$$：输出电容
$$C_{rss}$$：反向传输电容

且有：

$$C_{iss} = C_{gd}+C_{gs}$$
$$C_{oss} = C_{gd}+C_{ds}$$
$$C_{rss} = C_{gd}$$

查看典型的MOSFET的寄生电容曲线，随便找一款，IPP60R099P6：

| 属性                          | 参数值           |
| :---------------------------- | :--------------- |
| 漏源电压（Vdss）              | 600V             |
| 连续漏极电流（Id）（25°C 时） | 37.9A(Tc)        |
| 漏源导通电阻                  | 99mΩ @ 14.5A,10V |
| 最大功率耗散（Ta=25°C）       | 278W(Tc)         |

根据其规格书，寄生电容曲线如下：

<div  align="center">
<img src="./MOSFET寄生电容/IPP60R099P6-寄生电容.png" width = "50%" height = "50%" alt="PP60R099P6-寄生电容" align=center />
</div>

可以看到跟二极管，三极管等一样，基本上电容是随着电压升到而降低的（**但$$C_{rss}$$有拐点向上，为何？**）。

## 寄生电容的影响

开关速度，开关损耗

## 电容等效模型

因为这些寄生电容并不是定值的，而是随着电压变化而变化的，因此，在不同的性能评估过程中（比如：开关速度、开关损耗、开关驱动电荷），其等效的电容并不相等。

## 曲线拟合

文章《理解MOSFET时间相关及能量相关输出电容Coss(tr)和Coss(er)》中，就指出，因为$$C_{oss}$$不为定值，不可以使用积分，但其实应该也是可以的，只是要先将$$C_{oss}$$曲线拟合成函数，然后用定积分。

如下开始挑战：

参考及引用：

[1] Power MOSFET Electrical Characteristics. TOSHIBA
[2]理解MOSFET时间相关及能量相关输出电容Coss(tr)和Coss(er)-刘松-万国半导体元件(深圳)有限公司
