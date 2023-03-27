---
layout: post
title:  "NR PUSCH Repetition"
author: "Geoffrey Hou"
comments: true
tags: NR
excerpt_separator: <!--more-->
sticky: true
hidden: true
---

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>

翻译学习总结下NR PUSCH的Repetition相关协议内容。<!--more-->

## 时域资源分配
首先有协议上一长串关于时域资源分配的描述。下面内容都是协议的章节编号和翻译。
#### 6.1.2.1 Resource allocation in time domain
当UE被一个DCI或RAR UL grant或fallbackRAR UL grant调度发送一个TB（并且没有CSI上报），或者UE被一个DCI调度发送一个TB（并且有CSI上报）时，该DCI中的字段'*Time domain resource assignment*'的值$m$ 或者 该RAR UL grant或fallbackRAR UL grant中的字段*PUSCH time resource allocation*的值$m$，提供了一个资源分配表的行索引$m+1$（关于为什么是$m+1$？因为DCI中这个字段占用4bit，可以表示0至15，但是协议中定义的行索引是1至16，所以需要加1，不知道为什么直接定义行索引0至15）。确定使用哪个资源分配表的方法见协议38214/6.1.2.1.1。

这个索引行定义了PUSCH传输使用的一些参数，这些参数包括：slot偏移$K_2$，符号的起始和长度指示*SLIV*或直接给出起始符号*S*和符号长度*L*，PUSCH的映射类型，用于TBS determination的slot个数（如果资源分配表中存在参数*numberOfSlotsTBoMS*），和重复次数（如果资源分配表中存在参数*numberOfRepetitions*）。

当UE被一个DCI的'*CSI request*'字段调度发送一个有CSI上报没有TB的PUSCH时，该DCI的'*Time domain resource assignment*'字段值$m$，提供了一个资源分配表的行索引$m+1$。
这个索引行定义了：符号的起始和长度指示*SLIV*或直接给出起始符号*S*和符号长度*L*，PUSCH的映射类型，$K_2$的值通过下面公式得到：
$$
K_2=\max _j Y_j(m+1)
$$
这里的$Y_j, j=0, \ldots, N_{\text {Rep }}-1$是$N_{\text {Rep }}$触发的CSI上报设置，表示下面高层参数的相应列表实例：
- *reportSlotOffsetListDCI-0-2*或者*reportSlotOffsetListDCI-0-2-r17*（如果通过DCI format 0_2调度PUSCH，并且该配置了这个参数）；
- *reportSlotOffsetListDCI-0-1*或者*reportSlotOffsetListDCI-0-1-r17*（如果通过DCI format 0_1调度PUSCH，并且该配置了这个参数）；
- 如果上面两条都不满足，那么就是*reportSlotOffsetList*或者*reportSlotOffsetList-r17*。
上面的参数都在IE *CSI-ReportConfig*中。$Y_j(m+1)$是$Y_j$的第$m+1$个实例。

UE发送PUSCH的slot $K_s$和$K_2$有关，并且通过下面公式计算：
如果至少有一个调度小区的UE配置了参数*ca-SlotOffset*，计算如下：
$$
K_s=\left\lfloor n \right\rfloor
$$
$$
K_s=\left\lfloor n \cdot \frac{2^{\mu P U S C H}}{2^{\mu_{P D C C H}}}\right\rfloor+K_2+\left\lfloor\left(\frac{N_{\text {slot, offset, }, P D C C H}^{C A}}{2^{\mu_0 f f s e t, P D C C H}}-\frac{N_{\text {slot, offset, }, P U S C H}^{C A}}{2^{\mu_0 \text { offet }, \text { PUSCH }}}\right) \cdot 2^{\mu_{P U S C H}}\right\rfloor
$$
否则，计算如下：
$$
K_s=\left\lfloor n \cdot \frac{2^{\mu P U S C H}}{2^{\mu P D C C H}}\right\rfloor+K_2+K_{\text {offset }} \cdot \frac{2^{\mu \text { PUSCH }}}{2^{\mu_{\text {off set }}}}
$$
这里的$K_{\text {offset }}$见38213/4.2，$\mu_{K_{\text {offset }}}$是$K_{\text {offset }}$的子载波间隔配置，对FR1，取0。$n$是调度DCI的slot，$K_2$和PUSCH的参数集有关，$\mu_{\text {PUSCH}}$和$\mu_{\text {PDCCH}}$是PUSCH和PDCCH的子载波间隔配置，并且要求调度的DCI不是由TC-RNTI CRC加扰的DCI format 0_0。

$N_{\text {slot, offset, PDCCH }}^{\mathrm{CA}}$和$\mu_{\text {offset,PDCCH}}$是小区接收到的PDCCH的$N_{\text {slot, offset}}^{\mathrm{CA}}$和$\mu_{\text {offset}}$，由*ca-SlotOffset*配置。对应的PUSCH的参数由发送PUSCH的小区的参数*ca-SlotOffset*配置，见38211/4.5。

在确定时域资源分配时
- 对于DCI format 0_1调度的PUSCH，如果*pusch-RepTypeIndicatorDCI-0-1*配置为'pusch-RepTypeB'，UE采用PUSCH repetition Type B过程。
- 对于DCI format 0_2调度的PUSCH，如果*pusch-RepTypeIndicatorDCI-0-2*配置为'pusch-RepTypeB'，UE采用PUSCH repetition Type B过程。
- 否则，对于PDCCH或RAR UL grant或fallbackRAR UL grant调度的PUSCH，UE采用PUSCH repetition Type A过程。

在确定时域资源分配时
对于DCI format 0_1或DCI format 0_2调度的PUSCH，如果参数*numberOfSlotsTBoMS*存在并且取值大于1，那么UE采用TB processing over multiple slots过程。

对于PUSCH repetition Type A和TB processing over multiple slots，起始符号*S*相对于slot的起始位置，连续符号数*L*从*S*开始计数，*S* *L*和*SLIV*之间的关系为：
if $(L-1) \leq 7$，then
$$
SLIV=14 \cdot(L-1)+S
$$
else
$$
SLIV=14 \cdot(14-L+1)+(14-1-S)
$$
并且$0<L \leq 14-S$。

对于PUSCH repetition Type B，起始符号*S*相对于slot起始位置，连续符号数*L*从*S*开始技术，并且这两个参数由资源分配表中的*startSymbol*和*length*确定（也就是对PUSCH repetition Type B，不能通过*SLIV*的方式配置）。

对于PUSCH repetition Type A和TB processing over multiple slots，PUSCH映射类型可以配置为Type A或Type B，见38211/6.4.1.1.3，由索引行确定。
对于PUSCH repetition Type B，PUSCH映射类型只能是Type B。

这是协议定义合法的起始符号和符号长度组合。
![image](https://user-images.githubusercontent.com/115327603/227889228-a6e8fa32-fdc4-4719-8440-8f18b823753a.png)

对于TB processing over multiple slots，当使用C-RNTI，MCS-C-RNTI或CS-RNTI加扰CRC（NDI=1）的DCI format 0_1或0_2调度发送PUSCH时，有以下要求：
- 用于TBS determination的slot个数$N$由*numberOfSlotsTBoMS*指示。
- 如果资源分配表格中存在*numberOfRepetitions*，那么重复次数*K*等于*numberOfRepetitions*；否则$K=1$。
- 当UE支持TB processing over multiple slots的重复时，UE不希望$N \cdot K$超过32。

当UE配置$\mu=5$或6时，UE不希望通过一个或多个DCI在一个slot上调度超过一个PUSCH。

对于PUSCH repetition Type A，当使用C-RNTI，MCS-C-RNTI或CS-RNTI加扰CRC（NDI=1）的DCI format 0_1或0_2调度发送PUSCH时，有以下要求：
- 如果资源分配表格中存在*numberOfRepetitions*，那么重复次数$K$等于*numberOfRepetitions*。
- 或者如果UE配置了*pusch-AggregationFactor*，那么重复次数$K$等于*pusch-AggregationFactor*。
- 否则，$K=1$.
- 用于TBS determination的slot个数$N=1$。

对于PUSCH repetition type A，RAR UL grant调度发送PUSCH时，MCS信息字段的2 MSBs提供了一个codepoint，用来确定重复次数$K$，配合下面的表格使用（用于TBS determination的slot个数$N=1$）。
对于PUSCH repetition type A，TC RNTI加扰CRC的DCI format 0_0调度发送PUSCH时，MCS信息字段的2 MSBs提供了一个codepoint，用来确定重复次数$K$，配合下面的表格使用（用于TBS determination的slot个数$N=1$）。
![image](https://user-images.githubusercontent.com/115327603/227894911-46b3adbe-ad19-4896-824e-47dd7f9d87b0.png)

如果配置了*pusch-TimeDomainAllocationListForMultiPUSCH*，UE不希望配置*pusch-AggregationFactor*。

如果UE在pusch *TimeDomainAllocationListForMultiPUSCH*中配置有*extendedK2*，其中一个或多个行包含用于服务小区的UL BWP上的pusch的多个*SLIV*，则UE不应用pusch *AggregationFactor*（如果配置），在服务小区的UL BWP上转换为DCI格式0_1，并且UE不期望在pusch *TimeDomainAllocationListForMultiPUSCH*中配置*numberOfRepetitions*。

