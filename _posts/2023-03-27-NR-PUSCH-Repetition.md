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
