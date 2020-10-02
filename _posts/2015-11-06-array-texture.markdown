---
layout: post
title:  通过数组生成纹理
date:   2015-11-06 22:46:36
categories: technique
---

	/**
	*
	*将输入的数据转换成纹理对象输出
	*@param arrays 数组数据
	*@param width  生成纹理的宽度，即数组数据的宽度
	*@param height 生成纹理的高度，即数组数据的高度
	*@param gl     webgl上下文
	*	
	*@return texture webgl纹理对象
	**/
	function textureFromArray(arrays,width,height,gl){
	   var typed_array = new Float32Array(arrays);
           var texture = gl.createTexture();
           gl.bindTexture(gl.TEXTURE_2D,texture);
           gl.pixelStorei(gl.UNPACK_FLIP_Y_WEBGL, true);
           gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.NEAREST);//对于非2的次幂纹理，缩放有限制，具体请查官方文档
           gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.NEAREST);
           gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_S, gl.CLAMP_TO_EDGE);
           gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_T, gl.CLAMP_TO_EDGE);
           var float_ext = gl.getExtension("OES_texture_float");//开启浮点型插件
           gl.texImage2D(gl.TEXTURE_2D,0,gl.RGBA,width,height,0,gl.RGBA,gl.FLOAT,typed_array);
           gl.generateMipmap(gl.TEXTURE_2D);
           gl.bindTexture(gl.TEXTURE_2D,null);
	   return texture;
	}
