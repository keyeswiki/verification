第10课 触摸感应logo
===================

|Img|

.. _1实验说明:

1.实验说明：
------------

如果你有了Micro:bit主板，你可以在你的项目中使用金色的触摸感应logo作为另一个输入，这就像多了一个按钮。触摸感应采用的是电容式触摸传感器，当你手指按下（或触摸）它时，它就能感应到电场的微小变化----就像你的手机或平板电脑屏幕一样。当你触摸它，能控制Micro:bit板实现某个功能。

.. _2-准备:

2. 准备：
---------

（1）通过Micro USB线连接Micro:bit主板和电脑。 |image1|

（2）打开离线版本的Mu软件。

.. _3-课程代码:

3. 课程代码：
-------------

可以直接在Mu编译器上传教程中的代码，也可以手动在Mu编译器编写代码。

添加代码到Mu编译器的教程与下载代码的教程请阅读“开发环境设置”文件夹中的文件“Mu
Editor 编译器教程”。

::

   from microbit import *
   time = 0
   start = 0
   running = False

   while True:

       if button_a.was_pressed():
           running = True
           start = running_time()
       if button_b.was_pressed():
           if running:
               time += running_time() - start
           running = False
       if pin_logo.is_touched():
           if not running:
               display.scroll(int(time/1000))

       if running:
           display.show(Image.HEART)
           sleep(300)
           display.show(Image.HEART_SMALL)
           sleep(300)
       else:
           display.show(Image.ASLEEP)

.. _4-实验结果:

4. 实验结果：
-------------

按照之前的方式将代码下载到Micro:bit主板，Micro
USB数据线不要拔下来，利用Micro
USB数据线上电，按下按钮A开始秒表运行。当计时时，LED点阵屏上就会显示一个跳动的心脏。按按钮B停止，你可以随时启动和停止它，它会不断增加时间，就像一个真正的秒表。按下Micro:bit主板前面的金色LOGO标志，以秒为单位显示测量的时间。要将时间重置为零，请按Micro:bit主板背面的reset按钮。

.. _5-代码解释:

5. 代码解释：
-------------

（1）Micro:bit以毫秒(数千分一秒)记录它被启动的时间。这被称为运行时间。
（2）当你按下按钮A时，一个名为start的变量被设置为当前运行时间。
（3）当你按下按钮B时，开始时间将从新的运行时间中减去，以计算出从你启动秒表以来已经过去了多少时间。这个差异被加到总时间中，总时间存储在一个名为time的变量中。
（4）如果你按下金色LOGO图标，程序就会在LED显示屏上显示经过的总时间。它通过除以1000将时间从毫秒(千分之一秒)转换为秒。它使用整数除法运算符给出整数(整型)的结果。
（5）该程序还使用一个名为running的布尔变量来控制该程序。布尔变量只能有两个值:true或false。如果“running”为“true”，则表示秒表已经启动。如果“running”为假，则表示秒表未启动或已停止。
（6）如果“running”为真，则跳动的心脏循环显示在LED点阵屏。
（7）如果秒表已经停止，如果“running”为假时，当你按下金色LOGO图标时，它将只显示时间。
（8）如果秒表已经启动，如果“running”为真时，则确保只有按下按钮B时，时间变量才会更改，代码还可防止错误读数。

.. |Img| image:: ./media/img-20230324171739.png
.. |image1| image:: ./media/img-20230327154148.png
