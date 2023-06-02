---
layout: post
title:  "What-is-a-Clear-Channel-Assessment(CCA)"
author: "Geoffrey Hou"
comments: true
tags: WIFI
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

What is a Clear Channel Assessment (CCA)。<!--more-->

# What is a Clear Channel Assessment (CCA)

原文见https://www.extremenetworks.com/extreme-networks-blog/what-is-a-clear-channel-assessment-cca/

CSMA/CA协议利用一道防线来确保任何Wi-Fi无线电不会在另一个无线电已经在同一信道上传输时进行传输。802.11-2016标准定义了一种物理载波侦听(carrier sense)机制，用于确定射频 (RF) 介质是否繁忙。

物理载波侦听由所有未传输或接收的Wi-Fi无线电不断执行。当STA执行物理载波侦听时，它实际上是在侦听信道以查看是否有任何其他RF传输正在占用该信道。 物理载波侦听有两个目的：

- 第一个目的是确定帧传输是否是STA接收的入站。如果介质忙，无线电将尝试与传输同步。
- 第二个目的是在传输之前确定介质是否忙。在STA可以传输之前，介质必须是空闲的。

为了满足这两个物理载波侦听的要求，802.11设备使用*clear channel assessment (CCA)*来评估RF介质。CCA涉及在物理层监听RF传输。802.11无线电在收听RF介质时使用两个独立的CCA阈值。如图1所示，信号检测 (SD) 阈值用于识别来自另一个传输802.11无线电的任何802.11前同步码传输。前导码是802.11帧传输的物理层报头的组成部分。前导码用于发送和接收802.11无线电之间的同步。

![image-20230602103752109](https://github.com/geoffreyhou/geoffreyhou.github.io/assets/115327603/a664f4ee-01ea-48c7-a36a-84b685fd5ac7)



SD阈值有时称为前导码preamble载波侦听阈值。大多数802.11无线电检测和解码802.11前导码preamble的信号检测 (SD) 阈值在统计上约为4 dB信噪比 (SNR)。换句话说，802.11无线电通常可以在接收到的信号上以高于本底噪声约4 dB解码任何传入的802.11前导码传输。

能量检测 (ED) 阈值用于在空闲信道评估 (CCA) 期间检测任何其他类型的RF传输。请记住，2.4 GHz和5 GHz频段是免许可频段，其他非802.11 RF传输可能会占用一个信道。如图1所示，ED阈值比信号检测阈值高20 dB。例如，如果信道36的本底噪声为–95 dBm，则用于检测802.11传输的SD阈值约为–91 dBm，而用于检测其他RF传输的ED阈值为–71 dBm。如果信道40的本底噪声为–100 dBm，则用于检测802.11传输的SD阈值约为–96 dBm，而用于检测其他RF传输的ED阈值为–76 dBm。

这两个CCA阈值的定义在802.11-2016标准中有些模糊，这常常导致对实际阈值的误解。802.11客户端和AP无线电的WLAN制造商对这些阈值的解释通常会有所不同。更复杂的是，请记住无线电之间的接收灵敏度能力可能相差很大。 由于接收灵敏度的差异，本底噪声的感知在802.11无线电之间可能大不相同。因此，这两个CCA阈值也可能因无线电接收灵敏度的差异而有所不同。本博客中讨论的CCA阈值基于20 MHz信道上的传输。在讨论绑定40 MHz信道的主要和次要信道时CCA阈值的讨论变得更加复杂。
