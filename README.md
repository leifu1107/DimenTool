# DimenTool
Android 屏幕适配方案,自动生成不同分辨率的值
android中官方建议的屏幕适配方式，通过根据不同的分辨率在工程的res文件夹下建立不同的尺寸文件夹，每个文件夹下都建立dimens.xml文件。然后根据不同的尺寸在dimens.xml文件夹中分别计算配置不同的dp或者sp单位。开发中发现，android屏幕适配需要用到很多的尺寸，每个尺寸都建立dimens.xml问价。每个文件中的数值都要按照比例去计算，一个一个拿着计算器去计算吗？这样太麻烦了。今天有一个好的办法，来为大家介绍一下。

#### 效果图
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/2.png) 
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/1.png) 
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/3.png) 
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/4.png) 
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/5.png) 
