---
layout: post
title:  流线技术
date:   2015-10-24 10:06:14  
categories: technique
---

OLIC

稀疏噪声与ramp卷积核结合，可以同时展示流的方向和走向。

Enhanced LIC

LIC生成的图像作为下一轮LIC的输入，最后通过高通滤波器

在enhanced LIC中使用稀疏噪声，效果不同。

TexMap LIC

TexMap LIC利用纹理映射和缓冲区积累，两种opengl兼容硬件能力，来加速LIC图像生成。首先建立与流场同样分辨率的笛卡尔网格。网格根据流方向弯曲，噪声纹理平流通过纹理映射产生一系列中间纹理，传送到累积缓冲，那里是LIC图像通过纹理卷积最终生成的地方。可以使用白噪声或者稀疏噪声作为输入纹理。


