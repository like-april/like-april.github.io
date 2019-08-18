---
layout:     post
title:      "Matlab App Designer 笔记"
subtitle:   " \" Matlab App Designer note\""
date:       2019-08-18 16:01:00
author:     "张凡"
header-img: "https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab.jpg"
catalog: true
tags:
    - App Designer
    - Matlab
---

# Matlab App Designer 笔记

### 1、Matlab 使用 App Designer 的条件

​	Mathworks 在R2016a 中正式推出了GUIDE 的替代产品:AppDesigner，这是在MATLAB
图形系统转向使⽤⾯向对象系统之后(2014b)，⼀个重要的后续产品，它旨在顺应Web
的潮流, 帮助⽤户利⽤新的图形系统⽅便的设计更加美观的GUI。要使⽤App Designer，需
要最新的MATLAB R2016a及以上的版本。



### 2、App Designer  和 GUIDE的对比

相比于GUIDE的显著的特点如下所示：

```
- 最明显的特点：⾃动⽣成的代码使⽤了⾯向对象的语法。
- 最⼤的优点是：增加了和⼯业应⽤相关的控件：⽐如仪表盘，旋钮，开关，指⽰灯。
- 采⽤现代且友好的界⾯，⽤户更容易⾃⼰学习和探索。
```



### 3、App Designer 的简易使用

------

#### 3.1 在matlab中打开 App Designer

在matlab中打开App Designer有两种方法。

- 方法一

  在matlab命令行中输入 **appdesigner** 回车后就可以打开App Designer设计器。

- 方法二

  在matlab主页找到 **主页>新建>App设计工具**，然后点击打开，如下图所示：

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/openappdesigner.jpg)

  打开后的app designer设计界面如下图所示：

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner.png)

#### 3.2  App Designer GUI 简单的布局

##### 3.2.1 第一步，拖拽需要的控件到画布上

​	在App Designer的GUI设计中，通过拖拽相关的控件来完成GUI的简单布局，如下图所示，我们设计一个计算汇率转换的App，先将所需要的控件（用到了输入输出框、确定按钮这三个控件）拖拽带画布中（画布的大小可调）。

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner1.png)

##### 3.2.2 编辑和修改控件的相关参数	

​	将上述画布中相应控件的名称更改成我们需要的名称，直接点击相关的字段即可完成编辑修改，修改后的界面如下图所示：

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner2.png)

##### 3.3 编辑部分控件的回调函数

  	如上图所示，我们设计好了汇率转换这个测试App的界面，但是点击相关控件并不会有任何反应，这是因为还没有确定各个控件之间的逻辑和控制关系，而这些需要通过编写回调函数来实现。

​	我们上面设计的App界面实质上是在设计视图上看到的样子，如下图所示：

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner3.png)

​	点击代码视图，即可看到该App的描述代码，如下图所示，而我们的回调函数也正是在代码视图下编辑。设计视图和代码视图实质上是同一个东西的不同表现形式。

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner4.png)



**编辑 按钮 的回调函数**

​	在设计视图下，右键单击按钮，找到*回调  > 添加ButtonPushedFcn回调*，会转到代码视图的回调函数功能编辑区，直接编辑回调函数就可以了

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner5.png)



​	下面再3.4中讲如何实现汇率转换这个App的功能

##### 3.4 汇率转换App功能的实现

 	上面我们以汇率转换为例讲了回调函数的相关问题，接着上面的例子来，上面已经布局好了app的界面，接下来首先设置一个汇率变量参数x，在代码视图模式导航栏的编辑器中找到 *属性*，点击添加*私有属性*（也就是只能在当前类中使用，类似于局部变量）。在代码中生成的空白的properties 中 添加如下代码：

```matlab
x double
```

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner6.png)

其中代码当中的x为声明的属性，double为属性的类型。

​	回到设计视图，右键单击右侧边栏中的**app.UIFigure**的回调，选择**添加StartupFcn回调** 来给上面的汇率变量x赋初值。在StartupFcn的回调函数下添加如下代码完成对x的赋值：

```matlab
app.x=6.9;      %美元对人民币的汇率约为6.9左右
```

​	![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner7.png)

在Button的回调函数中添加如下代码：

```matlab
USD=app.EditField.Value;       %从第一个输入框获取输入的美元值
RMB=app.x*USD;                 %计算从美元到人民币的汇率转换
app.EditField_2.Value=RMB;     %把转换结果传到第二个输入框显示
```

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner8.png)

回调函数编写完成之后，点击导航栏中的运行，运行这个app，效果如下图中的动图所示：

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/huilvzhuanhuan.gif)

这个app的完整代码如下所示：

```matlab
classdef app1 < matlab.apps.AppBase

    % Properties that correspond to app components
    properties (Access = public)
        UIFigure          matlab.ui.Figure
        EditFieldLabel    matlab.ui.control.Label
        EditField         matlab.ui.control.NumericEditField
        EditField_2Label  matlab.ui.control.Label
        EditField_2       matlab.ui.control.NumericEditField
        Button            matlab.ui.control.Button
    end


    properties (Access = private)
        x double % Description
    end


    methods (Access = private)

        % Code that executes after component creation
        function startupFcn(app)
            app.x=6.9;   %美元对人民币的汇率约为6.9左右
        end

        % Button pushed function: Button
        function ButtonPushed(app, event)
            USD=app.EditField.Value;       %从第一个输入框获取输入的美元值
            RMB=app.x*USD;                 %计算从美元到人民币的汇率转换
            app.EditField_2.Value=RMB;     %把转换结果传到第二个输入框显示
        end
    end

    % App initialization and construction
    methods (Access = private)

        % Create UIFigure and components
        function createComponents(app)

            % Create UIFigure
            app.UIFigure = uifigure;
            app.UIFigure.Position = [100 100 253 282];
            app.UIFigure.Name = 'UI Figure';

            % Create EditFieldLabel
            app.EditFieldLabel = uilabel(app.UIFigure);
            app.EditFieldLabel.HorizontalAlignment = 'right';
            app.EditFieldLabel.Position = [73 206 29 22];
            app.EditFieldLabel.Text = '美元';

            % Create EditField
            app.EditField = uieditfield(app.UIFigure, 'numeric');
            app.EditField.Position = [117 206 100 22];

            % Create EditField_2Label
            app.EditField_2Label = uilabel(app.UIFigure);
            app.EditField_2Label.HorizontalAlignment = 'right';
            app.EditField_2Label.Position = [71 143 41 22];
            app.EditField_2Label.Text = '人民币';

            % Create EditField_2
            app.EditField_2 = uieditfield(app.UIFigure, 'numeric');
            app.EditField_2.Position = [127 143 100 22];

            % Create Button
            app.Button = uibutton(app.UIFigure, 'push');
            app.Button.ButtonPushedFcn = createCallbackFcn(app, @ButtonPushed, true);
            app.Button.Position = [68 62 127 37];
            app.Button.Text = '汇率转换';
        end
    end

    methods (Access = public)

        % Construct app
        function app = app1

            % Create and configure components
            createComponents(app)

            % Register the app with App Designer
            registerApp(app, app.UIFigure)

            % Execute the startup function
            runStartupFcn(app, @startupFcn)

            if nargout == 0
                clear app
            end
        end

        % Code that executes before app deletion
        function delete(app)

            % Delete UIFigure when app is deleted
            delete(app.UIFigure)
        end
    end
end
```



### 4、其他控件的使用

#### 4.1 图表（坐标区）控件的使用

​	我们经常见到在app中显示图表的问题，这里以绘制y=sin(x) 和 y=cos(x)的图像为例讲一下如何使用图表控件显示图。首先我们需要把坐标区控件拖拽到画布中合适的位置，再拖拽两个按钮（分别绘制y=sin(x) 和 y=cos(x)的图像）。

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner9.png)

​	和3.4中一样添加一个私有属性来定义一个变量x,并再引入回调函数StartupFcn来给x赋初值，如下所示：

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/appdesigner10.png)

下一步分别设置两个按钮的回调函数，在其中分别添加如下代码：

```matlab
% Button pushed function: ysinxButton
function ysinxButtonPushed(app, event)
	plot(app.UIAxes,app.x,sin(app.x));
end

% Button pushed function: ycosxButton
function ycosxButtonPushed(app, event)
	plot(app.UIAxes,app.x,cos(app.x));
end
```

不知道注意到了没有，要在坐标区控件中显示图的话，需要在plot()中添加**app.UIAxes** 这个语句。最后的效果如下面动图所示：

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/tubiaokongjian.gif)

​	完整代码如下所示：

```matlab
classdef app2 < matlab.apps.AppBase

    % Properties that correspond to app components
    properties (Access = public)
        UIFigure     matlab.ui.Figure
        UIAxes       matlab.ui.control.UIAxes
        ysinxButton  matlab.ui.control.Button
        ycosxButton  matlab.ui.control.Button
    end


    properties (Access = private)
        x double % Description
    end


    methods (Access = private)

        % Code that executes after component creation
        function startupFcn(app)
            app.x=0:0.01:2*pi;
        end

        % Button pushed function: ysinxButton
        function ysinxButtonPushed(app, event)
            plot(app.UIAxes,app.x,sin(app.x));
        end

        % Button pushed function: ycosxButton
        function ycosxButtonPushed(app, event)
            plot(app.UIAxes,app.x,cos(app.x));
        end
    end

    % App initialization and construction
    methods (Access = private)

        % Create UIFigure and components
        function createComponents(app)

            % Create UIFigure
            app.UIFigure = uifigure;
            app.UIFigure.Position = [100 100 487 416];
            app.UIFigure.Name = 'UI Figure';

            % Create UIAxes
            app.UIAxes = uiaxes(app.UIFigure);
            title(app.UIAxes, 'Title')
            xlabel(app.UIAxes, 'X')
            ylabel(app.UIAxes, 'Y')
            app.UIAxes.Box = 'on';
            app.UIAxes.XGrid = 'on';
            app.UIAxes.YGrid = 'on';
            app.UIAxes.TitleFontWeight = 'bold';
            app.UIAxes.Position = [55 86 389 296];

            % Create ysinxButton
            app.ysinxButton = uibutton(app.UIFigure, 'push');
            app.ysinxButton.ButtonPushedFcn = createCallbackFcn(app, @ysinxButtonPushed, true);
            app.ysinxButton.Position = [114 32 100 22];
            app.ysinxButton.Text = 'y=sin(x)';

            % Create ycosxButton
            app.ycosxButton = uibutton(app.UIFigure, 'push');
            app.ycosxButton.ButtonPushedFcn = createCallbackFcn(app, @ycosxButtonPushed, true);
            app.ycosxButton.Position = [308 32 100 22];
            app.ycosxButton.Text = 'y=cos(x)';
        end
    end

    methods (Access = public)

        % Construct app
        function app = app2

            % Create and configure components
            createComponents(app)

            % Register the app with App Designer
            registerApp(app, app.UIFigure)

            % Execute the startup function
            runStartupFcn(app, @startupFcn)

            if nargout == 0
                clear app
            end
        end

        % Code that executes before app deletion
        function delete(app)

            % Delete UIFigure when app is deleted
            delete(app.UIFigure)
        end
    end
end
```



#### 4.2 拨码开关和信号灯的使用



#### 4.3 仪表控件的使用



#### 4.4 旋钮的使用

 

