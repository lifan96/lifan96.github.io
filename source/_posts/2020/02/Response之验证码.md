---
title: Response之验证码
date: 2020-02-01 11:23:13
categories: Java
---

1. 步骤

   - 创建对象，在内存中生成图片（验证码图片对象）

   ```java
   int width = 100;
   int height = 50;
   
   BufferedImage image = new BufferedImage(width,height,BufferedImage.TYPE_INT_RGB);
   ```

   - 美化图片

   ```java
   //美化图片
           //填充背景色
           Graphics g = image.getGraphics();  //画笔对象
           g.setColor(Color.PINK);//设置背景色
           g.fillRect(0,0,width,height);
   
           //画边框
           g.setColor(Color.BLUE);
           g.drawRect(0,0,width-1,height-1);
   
           String str = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
           //生成随机下标
           Random ran = new Random();
           for (int i = 1; i <= 4; i++) {
               int index = ran.nextInt(str.length());
               //获取字符
               char ch = str.charAt(index);
   
               //写验证码
               g.drawString(ch+"",width/5*i,height/2);
           }
   
           //画干扰线
           g.setColor(Color.GREEN);
           //随机生成坐标点
           for (int i = 0; i < 10; i++) {
               int x1 = ran.nextInt(width);
               int x2 = ran.nextInt(width);
   
               int y1 = ran.nextInt(height);
               int y2 = ran.nextInt(height);
               g.drawLine(x1,y1,x2,y2);
           }
   ```

   - 将图片输出到页面

   ```java
    //将图片输出到页面展示
           ImageIO.write(image,"jpg",resp.getOutputStream());
   ```

   