---
layout: post
title:  JS单体模式
date:   2015-11-13 10:47:45
categories: js-mode
---

方式一：

	function Universe(){
		var instance;
		
		//
		Universe = function(){
			return instance;			
		}
		
		//
		Universe.prototype = this; 
		
		instance = new Universe();
		
		instance.constructor = Universe;
		
		instance.start_time = 0;
		instance.bang = "Big";
		return instance;
	}
	
方式二：

	var Universe2;
	(function(){ 
		var instance;
		Universe = function(){
			if(instance){
				return instance;
			}
			instance = this;
			this.start_time = 0;
			this.bang = "big";
		}
	}());