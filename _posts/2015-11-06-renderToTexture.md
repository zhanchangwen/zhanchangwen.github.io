---
layout: post
title:  渲染到纹理
date:   2015-11-06 10:06:14  
categories: webgl
---

转自：[http://learningwebgl.com/blog/?p=1786](http://learningwebgl.com/blog/?p=1786)


帧缓存可以用于渲染场景，它由各种各样位的存储构成。有一个默认的帧缓存，我们过去通常直接渲染到这个帧缓存，然后显示到网页上--但是你可以创造你自己的帧缓存，并渲染到这些帧缓存上。在这个教程中，我们将生成一个帧缓存，并告诉它，使用一个纹理作为位存储来保存颜色信息当它渲染时；我们同样需要为它分配空间用于深度计算。
帧缓存：包含渲染场景所需的全部信息，texture存颜色，renderBuffer存深度。

    
    function initTextureFramebuffer(gl){
        var framebuffer = gl.createFramebuffer();
        gl.bindFramebuffer(gl.FRAMEBUFFER, framebuffer);
        framebuffer.width = 512;
        framebuffer.height = 512;
    
        framebuffer.texture = gl.createTexture();
        gl.bindTexture(gl.TEXTURE_2D, framebuffer.texture);
        gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.LINEAR);
        gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.LINEAR_MIPMAP_NEAREST);
        gl.generateMipmap(gl.TEXTURE_2D);
    
        gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, framebuffer.width, framebuffer.height, 0, gl.RGBA, gl.UNSIGNED_BYTE, null);
        framebuffer.renderbuffer = gl.createRenderbuffer();
        gl.bindRenderbuffer(gl.RENDERBUFFER, framebuffer.renderbuffer);
        gl.renderbufferStorage(gl.RENDERBUFFER, gl.DEPTH_COMPONENT16, framebuffer.width, framebuffer.height);
    
        gl.framebufferTexture2D(gl.FRAMEBUFFER, gl.COLOR_ATTACHMENT0, gl.TEXTURE_2D, framebuffer.texture, 0);
        gl.framebufferRenderbuffer(gl.FRAMEBUFFER, gl.DEPTH_ATTACHMENT, gl.RENDERBUFFER, framebuffer.renderbuffer);
    
        gl.bindTexture(gl.TEXTURE_2D, null);
        gl.bindRenderbuffer(gl.RENDERBUFFER, null);
        gl.bindFramebuffer(gl.FRAMEBUFFER, null);
        return framebuffer;
    }
