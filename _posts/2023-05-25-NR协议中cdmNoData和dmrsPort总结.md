---
layout: post
title:  "NR协议中cdmNoData和dmrsPort总结"
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

NR协议中cdmNoData和dmrsPort总结。<!--more-->

如果做DFT，那么cdmGrpNoData=2。

如果不做DFT，

- 如果dmrsCfgType=1，dmrsLen=1，layerNum=1，
	- 如果dmrsPort0=0，cdmGrpNoData=1、2。
	- 如果dmrsPort0=1，cdmGrpNoData=1、2。
	- 如果dmrsPort0=2，cdmGrpNoData=2。
	- 如果dmrsPort0=3，cdmGrpNoData=2。
- 如果dmrsCfgType=1，dmrsLen=1，layerNum=2，
	- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2。
	- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2。
	- 如果dmrsPort0=0，dmrsPort1=2，cdmGrpNoData=2。
- 如果dmrsCfgType=1，dmrsLen=1，layerNum=1，
	- 如果dmrsPort0=0，cdmGrpNoData=1、2。
	- 如果dmrsPort0=1，cdmGrpNoData=1、2。
	- 如果dmrsPort0=2，cdmGrpNoData=2。
	- 如果dmrsPort0=3，cdmGrpNoData=2。
- 如果dmrsCfgType=1，dmrsLen=2，layerNum=1，
	- 如果dmrsPort0=0，cdmGrpNoData=2。
	- 如果dmrsPort0=1，cdmGrpNoData=2。
	- 如果dmrsPort0=2，cdmGrpNoData=2。
	- 如果dmrsPort0=3，cdmGrpNoData=2。
	- 如果dmrsPort0=4，cdmGrpNoData=2。
	- 如果dmrsPort0=5，cdmGrpNoData=2。
	- 如果dmrsPort0=6，cdmGrpNoData=2。
	- 如果dmrsPort0=7，cdmGrpNoData=2。
- 如果dmrsCfgType=1，dmrsLen=1，layerNum=2，
	- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2。
	- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2。
	- 如果dmrsPort0=0，dmrsPort1=2，cdmGrpNoData=2。
- 如果dmrsCfgType=1，dmrsLen=2，layerNum=2，
	- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=2。
	- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2。
	- 如果dmrsPort0=4，dmrsPort1=5，cdmGrpNoData=2。
	- 如果dmrsPort0=6，dmrsPort1=7，cdmGrpNoData=2。
	- 如果dmrsPort0=0，dmrsPort1=4，cdmGrpNoData=2。
	- 如果dmrsPort0=2，dmrsPort1=6，cdmGrpNoData=2。
- 如果dmrsCfgType=2，dmrsLen=1，layerNum=1，
	- 如果dmrsPort0=0，cdmGrpNoData=1、2、3。
	- 如果dmrsPort0=1，cdmGrpNoData=1、2、3。
	- 如果dmrsPort0=2，cdmGrpNoData=2、3。
	- 如果dmrsPort0=3，cdmGrpNoData=2、3。
	- 如果dmrsPort0=4，cdmGrpNoData=3。
	- 如果dmrsPort0=5，cdmGrpNoData=3。

- 如果dmrsCfgType=2，dmrsLen=1，layerNum=2，
	- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2、3。
	- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2、3。
	- 如果dmrsPort0=4，dmrsPort1=5，cdmGrpNoData=3。
	- 如果dmrsPort0=0，dmrsPort1=2，cdmGrpNoData=2。
- 如果dmrsCfgType=2，dmrsLen=1，layerNum=1，
	- 如果dmrsPort0=0，cdmGrpNoData=1、2、3。
	- 如果dmrsPort0=1，cdmGrpNoData=1、2、3。
	- 如果dmrsPort0=2，cdmGrpNoData=2、3。
	- 如果dmrsPort0=3，cdmGrpNoData=2、3。
	- 如果dmrsPort0=4，cdmGrpNoData=3。
	- 如果dmrsPort0=5，cdmGrpNoData=3。
- 如果dmrsCfgType=2，dmrsLen=2，layerNum=1，
	- 如果dmrsPort0=0，cdmGrpNoData=3。
	- 如果dmrsPort0=1，cdmGrpNoData=3。
	- 如果dmrsPort0=2，cdmGrpNoData=3。
	- 如果dmrsPort0=3，cdmGrpNoData=3。
	- 如果dmrsPort0=4，cdmGrpNoData=3。
	- 如果dmrsPort0=5，cdmGrpNoData=3。
	- 如果dmrsPort0=6，cdmGrpNoData=3。
	- 如果dmrsPort0=7，cdmGrpNoData=3。
	- 如果dmrsPort0=8，cdmGrpNoData=3。
	- 如果dmrsPort0=9，cdmGrpNoData=3。
	- 如果dmrsPort0=10，cdmGrpNoData=3。
	- 如果dmrsPort0=11，cdmGrpNoData=3。
	- 如果dmrsPort0=0，cdmGrpNoData=1。
	- 如果dmrsPort0=1，cdmGrpNoData=1。
	- 如果dmrsPort0=6，cdmGrpNoData=1。
	- 如果dmrsPort0=7，cdmGrpNoData=1。

- 如果dmrsCfgType=2，dmrsLen=1，layerNum=2，
	- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2、3。
	- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2、3。
	- 如果dmrsPort0=4，dmrsPort1=5，cdmGrpNoData=3。
	- 如果dmrsPort0=0，dmrsPort1=2，cdmGrpNoData=2。
- 如果dmrsCfgType=2，dmrsLen=2，layerNum=2，
	- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2、3。
	- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2、3。
	- 如果dmrsPort0=4，dmrsPort1=5，cdmGrpNoData=3。
	- 如果dmrsPort0=6，dmrsPort1=7，cdmGrpNoData=1、2、3。
	- 如果dmrsPort0=8，dmrsPort1=9，cdmGrpNoData=2、3。
	- 如果dmrsPort0=10，dmrsPort1=11，cdmGrpNoData=3。



稍微整理下。

如果dmrsCfgType=1，dmrsLen=1，layerNum=1，

- 如果dmrsPort0=0，cdmGrpNoData=1、2。
- 如果dmrsPort0=1，cdmGrpNoData=1、2。
- 如果dmrsPort0=2，cdmGrpNoData=2。
- 如果dmrsPort0=3，cdmGrpNoData=2。

如果dmrsCfgType=1，dmrsLen=1，layerNum=2，

- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2。
- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2。
- 如果dmrsPort0=0，dmrsPort1=2，cdmGrpNoData=2。

如果dmrsCfgType=1，dmrsLen=2，layerNum=1，

- 如果dmrsPort0=0，cdmGrpNoData=2。
- 如果dmrsPort0=1，cdmGrpNoData=2。
- 如果dmrsPort0=2，cdmGrpNoData=2。
- 如果dmrsPort0=3，cdmGrpNoData=2。
- 如果dmrsPort0=4，cdmGrpNoData=2。
- 如果dmrsPort0=5，cdmGrpNoData=2。
- 如果dmrsPort0=6，cdmGrpNoData=2。
- 如果dmrsPort0=7，cdmGrpNoData=2。

如果dmrsCfgType=1，dmrsLen=2，layerNum=2，

- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=2。
- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2。
- 如果dmrsPort0=4，dmrsPort1=5，cdmGrpNoData=2。
- 如果dmrsPort0=6，dmrsPort1=7，cdmGrpNoData=2。
- 如果dmrsPort0=0，dmrsPort1=4，cdmGrpNoData=2。
- 如果dmrsPort0=2，dmrsPort1=6，cdmGrpNoData=2。

也就是，

如果dmrsCfgType=1，dmrsLen=1，layerNum=1，（如果只用cdm0，可以配置cdmGrpNoData=1、2；如果只用cdm1，可以配置cdmGrpNoData=2）

- 如果dmrsPort0=0，cdmGrpNoData=1、2。1个cdm组，cdm0
- 如果dmrsPort0=1，cdmGrpNoData=1、2。1个cdm组，cdm0
- 如果dmrsPort0=2，cdmGrpNoData=2。1个cdm组，cdm1
- 如果dmrsPort0=3，cdmGrpNoData=2。1个cdm组，cdm1

如果dmrsCfgType=1，dmrsLen=1，layerNum=2，（如果只用cdm0，可以配置cdmGrpNoData=1、2；如果只用cdm1，可以配置cdmGrpNoData=2；如果cdm0和cdm1都用，可以配置cdmGrpNoData=2）

- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2。1个cdm组，cdm0
- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2。1个cdm组，cdm1
- 如果dmrsPort0=0，dmrsPort1=2，cdmGrpNoData=2。2个cdm组，cdm0，cdm1

上面两个合并就是：

如果dmrsCfgType=1，dmrsLen=1，

- 如果只用cdm0，可以配置cdmGrpNoData=1、2；

- 如果只用cdm1，就只能配置cdmGrpNoData=2；
- 如果同时使用cdm0和cdm1，就只能配置cdmGrpNoData=2；

如果dmrsCfgType=1，dmrsLen=2，

- cdmGrpNoData=2。



如果dmrsCfgType=2，dmrsLen=1，layerNum=1，（如果只用cdm0，可以配置cdmGrpNoData=1、2、3；如果只用cdm1，可以配置cdmGrpNoData=2、3；如果只用cdm2，可以配置cdmGrpNoData=3；）

- 如果dmrsPort0=0，cdmGrpNoData=1、2、3。（cdm0）
- 如果dmrsPort0=1，cdmGrpNoData=1、2、3。（cdm0）
- 如果dmrsPort0=2，cdmGrpNoData=2、3。（cdm1）
- 如果dmrsPort0=3，cdmGrpNoData=2、3。（cdm1）
- 如果dmrsPort0=4，cdmGrpNoData=3。（cdm2）
- 如果dmrsPort0=5，cdmGrpNoData=3。（cdm2）

如果dmrsCfgType=2，dmrsLen=1，layerNum=2，（如果只用cdm0，可以配置cdmGrpNoData=1、2、3；如果只用cdm1，可以配置cdmGrpNoData=2、3；如果只用cdm2，可以配置cdmGrpNoData=3；如果同时使用cdm0和cdm1，可以配置cdmGrpNoData=2）

- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2、3。（cdm0）
- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2、3。（cdm1）
- 如果dmrsPort0=4，dmrsPort1=5，cdmGrpNoData=3。（cdm2）
- 如果dmrsPort0=0，dmrsPort1=2，cdmGrpNoData=2。（cdm0、cdm1）

如果dmrsCfgType=2，dmrsLen=2，layerNum=1，（如果只用cdm0，可以配置cdmGrpNoData=1、3；如果只用cdm1，可以配置cdmGrpNoData=3；如果只用cdm2，可以配置cdmGrpNoData=3；）

- 如果dmrsPort0=0，cdmGrpNoData=1、3。（cdm0）
- 如果dmrsPort0=1，cdmGrpNoData=1、3。（cdm0）
- 如果dmrsPort0=2，cdmGrpNoData=3。（cdm1）
- 如果dmrsPort0=3，cdmGrpNoData=3。（cdm1）
- 如果dmrsPort0=4，cdmGrpNoData=3。（cdm2）
- 如果dmrsPort0=5，cdmGrpNoData=3。（cdm2）
- 如果dmrsPort0=6，cdmGrpNoData=1、3。（cdm0）
- 如果dmrsPort0=7，cdmGrpNoData=1、3。（cdm0）
- 如果dmrsPort0=8，cdmGrpNoData=3。（cdm1）
- 如果dmrsPort0=9，cdmGrpNoData=3。（cdm1）
- 如果dmrsPort0=10，cdmGrpNoData=3。（cdm2）
- 如果dmrsPort0=11，cdmGrpNoData=3。（cdm2）

如果dmrsCfgType=2，dmrsLen=2，layerNum=2，（如果只用cdm0，可以配置cdmGrpNoData=1、2、3；如果只用cdm1，可以配置cdmGrpNoData=2、3；如果只用cdm2，可以配置cdmGrpNoData=3；）

- 如果dmrsPort0=0，dmrsPort1=1，cdmGrpNoData=1、2、3。（cdm0）
- 如果dmrsPort0=2，dmrsPort1=3，cdmGrpNoData=2、3。（cdm1）
- 如果dmrsPort0=4，dmrsPort1=5，cdmGrpNoData=3。（cdm2）
- 如果dmrsPort0=6，dmrsPort1=7，cdmGrpNoData=1、2、3。（cdm0）
- 如果dmrsPort0=8，dmrsPort1=9，cdmGrpNoData=2、3。（cdm1）
- 如果dmrsPort0=10，dmrsPort1=11，cdmGrpNoData=3。（cdm2）



如果dmrsCfgType=2，dmrsLen=1，layerNum=1，

- 如果只用cdm0，可以配置cdmGrpNoData=1、2、3；如果只用cdm1，可以配置cdmGrpNoData=2、3；如果只用cdm2，可以配置cdmGrpNoData=3；

如果dmrsCfgType=2，dmrsLen=1，layerNum=2，

- 如果只用cdm0，可以配置cdmGrpNoData=1、2、3；如果只用cdm1，可以配置cdmGrpNoData=2、3；如果只用cdm2，可以配置cdmGrpNoData=3；如果同时使用cdm0和cdm1，可以配置cdmGrpNoData=2

如果dmrsCfgType=2，dmrsLen=2，layerNum=1，（这个时候不能配置cdmGrpNoData=2）

- 如果只用cdm0，可以配置cdmGrpNoData=1、3；如果只用cdm1，可以配置cdmGrpNoData=3；如果只用cdm2，可以配置cdmGrpNoData=3；

如果dmrsCfgType=2，dmrsLen=2，layerNum=2，

- 如果只用cdm0，可以配置cdmGrpNoData=1、2、3；如果只用cdm1，可以配置cdmGrpNoData=2、3；如果只用cdm2，可以配置cdmGrpNoData=3；



总结起来，

- 如果只用cdm0，可以配置cdmGrpNoData=1、2、3（除了dmrsCfgType=2，dmrsLen=2，layerNum=1的场景，这个时候不能配置cdmGrpNoData=2）；
- 如果只用cdm1，可以配置cdmGrpNoData=2、3（除了dmrsCfgType=2，dmrsLen=2，layerNum=1的场景，这个时候不能配置cdmGrpNoData=2）；
- 如果只用cdm2，可以配置cdmGrpNoData=3；
- 如果同时使用cdm0和cdm1，可以配置cdmGrpNoData=2；







如果做DFT，那么cdmGrpNoData=2。并且只能配置dmrsCfgType=1。

如果不做DFT，

- 如果dmrsCfgType=1，
	- dmrsLen=1，
		- 如果只用cdm0，可以配置cdmGrpNoData=1、2；
		- 如果只用cdm1，就只能配置cdmGrpNoData=2；
		- 如果同时使用cdm0和cdm1，就只能配置cdmGrpNoData=2；
	- dmrsLen=2，
		- cdmGrpNoData=2。

- 如果dmrsCfgType=2，
	- 如果只用cdm0，可以配置cdmGrpNoData=1、2、3（除了dmrsCfgType=2，dmrsLen=2，layerNum=1的场景，这个时候不能配置cdmGrpNoData=2）；
	- 如果只用cdm1，可以配置cdmGrpNoData=2、3（除了dmrsCfgType=2，dmrsLen=2，layerNum=1的场景，这个时候不能配置cdmGrpNoData=2）；
	- 如果只用cdm2，只能配置cdmGrpNoData=3；
	- 如果同时使用cdm0和cdm1，只能配置cdmGrpNoData=2；
