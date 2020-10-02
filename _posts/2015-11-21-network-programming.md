---
layout: post
title:  网络编程
date:   2015-11-21 10:44:20
categories: java
---

InetAddress
---
 代表ip地址对象

URLDecoder URLEncoder 
---
用于普通中文字符串与application/x-www.form-urlencoded MIME字符串的转换
中文字符 转换成 "%xx%xx"
正向转换：URLEncoder.encode(String s,String enc)
反向转换：URLDecoder.decode(String s,String enc)

URL URLConnection URLPermission
---

创建URL连接，请求、读取的步骤：

1. 创建URL对象
2. 调用URL对象的openConnection()方法来创建URLConnection对象
3. 设置URLConnection的请求参数和普通请求属性
4. 若为"GET",则使用connect()方法建立和远程资源的实际连接即可；若为"POST"，则需要获取URLConnection实例对应的输出流来发送请求参数
5. 远程资源变为可用，程序可以访问__远程资源__的头字段或通过__输入输出流__读取远程资源的数据
  

DownUtil实现多线程下载的步骤
1. 创建URL对象
2. 获取制定URL对象指向资源的大小
3. 在本地磁盘创建一个与网络资源具有相同大小的空文件
4. 计算每个线程应该下载网络资源的哪个部分
5. 一次创建、启动多个线程来下载网络资源的指定部分

代码:多线程下载网上图片

	package lesson17;
	
	import java.io.IOException;
	import java.io.InputStream;
	import java.io.RandomAccessFile;
	import java.net.HttpURLConnection;
	import java.net.MalformedURLException;
	import java.net.URL;
	
	public class DownUtil {
		private String path;
		private String targetFile;
		private int threadNum;
		private DownThread[] threads;
		private int fileSize;
		public DownUtil(String path,String targetFile,int threadNum){
			this.path = path;
			this.targetFile = targetFile;
			this.threadNum = threadNum;
			threads = new DownThread[threadNum];
		}
		public void download(){
			try {
				URL url = new URL(path);
				HttpURLConnection conn = (HttpURLConnection) url.openConnection();
				conn.setConnectTimeout(5*1000);
				conn.setRequestMethod("GET");
				conn.setRequestProperty("Accept", "*/*");
				conn.setRequestProperty("Accept-Language", "zh-CN");
				conn.setRequestProperty("Charset", "UTF-8");
				conn.setRequestProperty("Connection", "Keep-Alive");
				fileSize = conn.getContentLength();
				conn.disconnect();
				int currentPartSize = fileSize/threadNum + 1;
				RandomAccessFile file = new RandomAccessFile(targetFile,"rw");
				file.setLength(fileSize);
				file.close();
				for(int i=0;i<threadNum;i++){
					int startPos = i * currentPartSize;
					RandomAccessFile currentPart = new RandomAccessFile(targetFile,"rw");
					currentPart.seek(startPos);
					threads[i] = new DownThread(startPos,currentPartSize,currentPart);
					threads[i].start();
				}
			} catch (MalformedURLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} finally {
			}
			
		}
		public double getCompleteRate(){
			int sumSize = 0;
			for(DownThread t:threads){
				sumSize += t.length;
			}
			return sumSize * 1.0 / fileSize;
		
		}
		private class DownThread extends Thread{
			private int startPos;
			private int currentPartSize;
			private RandomAccessFile currentPart;
			public int length;
			public DownThread(int startPos,int currentPartSize,RandomAccessFile currentPart){
				this.startPos = startPos;
				this.currentPart = currentPart;
				this.currentPartSize = currentPartSize;
			}
			public void run(){
				URL url;
				try {
					url = new URL(path);
					HttpURLConnection conn = (HttpURLConnection) url.openConnection();
					conn.setConnectTimeout(5*1000);
					conn.setRequestMethod("GET");
					conn.setRequestProperty("Accept", "*/*");
					conn.setRequestProperty("Accept-Language", "zh-CN");
					conn.setRequestProperty("Charset", "UTF-8");
					conn.setRequestProperty("Connection", "Keep-Alive");
					InputStream is = conn.getInputStream();
					is.skip(this.startPos);
					int hasRead = 0;
					byte[] buffer = new byte[1024];
					while(length < currentPartSize && 
							(hasRead = is.read(buffer)) != -1){
						currentPart.write(buffer,0,hasRead);
						length += hasRead;
					}
					currentPart.close();
					is.close();
				} catch (MalformedURLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}finally{
					
				}
			}
		}
	}

测试类：

	package lesson17;
	
	public class MultiThreadDown {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			System.out.println("hello world");
			String path = "http://c.hiphotos.baidu.com/image/pic/item/0d338744ebf81a4cab9f89c9d52a6059252da605.jpg";
			String filePath = "io.jpg";
			int numThreads = 4;
			final DownUtil downUtil = new DownUtil(path,filePath,numThreads);
			downUtil.download();
			PercentageThread pt = new PercentageThread(downUtil);
			pt.start();
		}
	}
	class PercentageThread extends Thread{
		private DownUtil util;
		public PercentageThread(DownUtil util){
			this.util = util;
		}
		public void run(){
			while(util.getCompleteRate() < 1){
				System.out.println("已完成"+util.getCompleteRate());
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		}
	}
	
	
	
