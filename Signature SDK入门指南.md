# 入门指南 

## 测试环境

Windows 7及以上版本提供了多种示例。

要测试这些样本，可以使用Wacom设备，如STU-500或DTU-1141等笔/平板设备。

使用笔/平板设备,您需要安装Wacom驱动程序,它提供签名库使用的wintab接口。
设备安装常见问题:
https://developer-docs.wacom.com/display/DevDocs/WILL+SDK+-+FAQs


## 下载 Signature SDK

SDK下载地址： https://developer.wacom.com/developer-dashboard

* 登录你的 Wacom ID
* 选择 **Downloads for signature**
* 下载 **Signature SDK for Windows Desktop**
* 接受使用SDK的最终用户许可协议

下载的Zip文件包含SDK文档。
Zip文件中的 'SignatureSDK' 文件夹含有 Signature Library 的 MSI 安装包.

## 安装 Signature SDK

无论你的Windows系统是32或64位, 对于入门者我们建议安装32位签名库:
**Wacom-Signature-SDK-x86-vXX.msi**

这将有助于以后在Internet Explore中打开html示例，因为默认情况下启动的是32位版本。
混合32/64位应用程序和组件的冲突是一个常见的支持问题。

运行安装程序使用默认选项来安装 Signature Library 到:
C:\Program Files (x86)\Common Files\WacomGSS

Signature Library 包括:
* COM DLLs
* licensing DLLs
* support DLLs
* language translations

----
## Signature Library 许可

要使用Signature Library，应用程序代码中必须包含许可证字符串。
许可证计划最近已放宽，标准许可可免费使用所有功能，但不包括:
- signature encryption
- ISO signature formatting

### Signature Library 标准许可

标准签名库许可证为JSON Web Token (JWT)格式，可在此复制:

```
eyJhbGciOiJSUzUxMiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiI3YmM5Y2IxYWIxMGE0NmUxODI2N2E5MTJkYTA2ZTI3NiIsImV4cCI6MjE0NzQ4MzY0NywiaWF0IjoxNTYwOTUwMjcyLCJyaWdodHMiOlsiU0lHX1NES19DT1JFIiwiU0lHQ0FQVFhfQUNDRVNTIl0sImRldmljZXMiOlsiV0FDT01fQU5ZIl0sInR5cGUiOiJwcm9kIiwibGljX25hbWUiOiJTaWduYXR1cmUgU0RLIiwid2Fjb21faWQiOiI3YmM5Y2IxYWIxMGE0NmUxODI2N2E5MTJkYTA2ZTI3NiIsImxpY191aWQiOiJiODUyM2ViYi0xOGI3LTQ3OGEtYTlkZS04NDlmZTIyNmIwMDIiLCJhcHBzX3dpbmRvd3MiOltdLCJhcHBzX2lvcyI6W10sImFwcHNfYW5kcm9pZCI6W10sIm1hY2hpbmVfaWRzIjpbXX0.ONy3iYQ7lC6rQhou7rz4iJT_OJ20087gWz7GtCgYX3uNtKjmnEaNuP3QkjgxOK_vgOrTdwzD-nm-ysiTDs2GcPlOdUPErSp_bcX8kFBZVmGLyJtmeInAW6HuSp2-57ngoGFivTH_l1kkQ1KMvzDKHJbRglsPpd4nVHhx9WkvqczXyogldygvl0LRidyPOsS5H2GYmaPiyIp9In6meqeNQ1n9zkxSHo7B11mp_WXJXl0k1pek7py8XYCedCNW5qnLi4UCNlfTd6Mk9qz31arsiWsesPeR9PN121LBJtiPi023yQU8mgb9piw_a-ccciviJuNsEuRDN3sGnqONG3dMSA
```
在示例中，使用上面的许可证替换搜索到的`<<license>>`字符串。

若要使用被排除的功能，请联系技术支持以获得合适的示例代码和许可证:
[developer relations portal.](https://developer.wacom.com/developer-dashboard/support)

## 示例代码

提供的示例代码中含有许可码占位符。
在使用所有sample之前请使用上面的标准许可码替换示例代码中的所有 `<<license>>`字符串。


## JavaScript Samples

要演示Signature Library，可以使用Windows本地的标准工具，特别是脚本主机CSCRIPT.EXE。
在64位Windows系统上，32位和64位应用程序有各自的版本。运行的版本决定了ActiveX控件的类型。
 
在64位Windows中:
  C:\Windows\SysWOW64\cscript.exe
在32位Windows:
  C:\Windows\cscript.exe

在示例中，批处理文件RUN-JS.bat自动启动cscript.exe的32位版本，例如:
```
Run-JS.bat CaptureImage.js
```

Javascript代码可以很容易地被移植到VB和c#，只需要进行少量的语法更改。



### 捕获签名

Signature Library最基本的用途是捕获签名。它的API是:

```ruby
  sigCtl = new ActiveXObject("Florentis.SigCtl");
  sigCtl.Licence = "<<license>>";
  dynCapt = new ActiveXObject("Florentis.DynamicCapture");
  rc = dynCapt.Capture(sigCtl,"Who","Why");
```

有关调用的详细信息，请参阅SDK中的COM API文档。
运行sample **CaptureImage.js**  来捕获一个签名:
```
Run-JS.bat CaptureImage.js
```

签名捕获窗口将会显示。它的布局和位置是不可配置的，原因是必须执行一致的签名体验。
不过，可以通过注册表设置和属性进行一些较小的更改，比如油墨颜色。这些选项都记录在签名库COM API中。
例如，要指定红墨水:
```
  dynCapt.SetProperty("CaptureInkColor","1.0,0,0");
```

![signature capture](images/SigCaptureAPI.png)



### 创建签名图片

捕获签名之后，您的应用程序将拥有一个签名对象，其中包含上下文信息(谁/为什么等)以及笔数据(x/y/p数据)。
使用RenderBitmap API创建一个图片:
```
  flags = 0x1000 | 0x80000 | 0x400000;    //SigObj.outputFilename | SigObj.color32BPP | SigObj.encodeData
  rc = sigCtl.Signature.RenderBitmap(filename, 300, 150, "image/png", 0.5, 0xff0000, 0xffffff, 0.0, 0.0, flags );
```
有关调用的详细信息，请参阅SDK中的COM API文档。
在本例中，使用提供给调用的flags设置确定的编码数据创建PNG图像。
'encoded data' 设置的作用是在签字图片中包含二进制签名对象。 
使用'隐写术'将二进制数据编码到图像中，使其不能立即可见，但却能被检索到。

### 保存和加载签名
  
使用编码数据创建的签名图像包含所有签名数据。
只要图像没有以任何方式改变，数据就可以加载到一个新的签名对象中。
这在示例**DecodeImage.js**中得到了演示:
```ruby
  sigCtl = new ActiveXObject("Florentis.SigCtl");
  sig = sigCtl.Signature;
  rc = sig.ReadEncodedBitmap(filename);
```
运行sample加载 sig.png:
```
Run-JS.bat DecodeImage.js
```

通信和保存签名对象的一种方便方法是通过SigText属性。
read/write 属性可用于保存和加载签名。
SigText是签名对象的base64 ascii文本编码，可以保存在数据库中，也可以提交给url，而无需考虑数据转换。
下面的示例创建文件sig.txt:

```
Run-JS.bat CaptureSigText.js
```

这个示例读取txt文件并生成一个签名图像sig.txt.png:
```
Run-JS.bat DecodeSigText.js
```

### 向导控件（Wizard Control）

向导控件是签名控件的一个扩展，专门针对STU签名板。
该向导控件引导用户通过一组指令页，这些指令页显示在签名板LCD显示屏上，每一页都需要通过笔尖点击进行选择，例如选择“Next”按钮。

指令页被脚本化以显示以下组合:

* 通用指示和指导文本
* 图像 
* 输入控制：
    * 单选按钮
    * 复选框
    * PIN 码输入
    * 控制按钮
* 绘制简单线条
* 签名捕捉

在PC显示器上，所有这些都可以通过使用普通的Windows控件来实现，例如Windows窗体。然而，STU显示不能直接被Windows访问，向导控件克服了这一限制。


#### WizardScript.js

该脚本演示了使用向导控件的原则，显示带有签名捕获的指令页:

```
Run-JS.bat WizardScipt.js
```

#### WIzardUpload.js

脚本演示了上传图像到STU显示:

```
Run-JS.bat WizardUpload.js stu\640x480.png
```

----
## HTML Samples

HTML/JavaScript示例只能在Internet Explorer中使用，因为需要ActiveX支持，而且出于安全原因，在其他浏览器中会特别屏蔽它。 但是，可以使用HTML示例来研究API，而不需要使用Visual Studio之类的开发系统，因为可以使用简单的文本编辑器来修改代码。
请注意，要在不同的浏览器(如Firefox或Chrome)中使用签名库，需要额外的服务：请参阅跨浏览器支持的签名库SigCaptX。

在Internet Explorer —— 唯一支持ActiveX的浏览器 中打开html示例。

在IE中，你必须“允许被阻止的内容”，提示允许ActiveX控件运行。
你可以通过IE设置消除提示：IE工具 —— Internet 选项 —— 高级 —— 安全：允许活动内容

如果你安装的64位版本的签名库，你需要运行64位的Internet Explorer。
If you installed the 64-bit version of the Signature Library you will need to run the 64-bit version of Internet Explorer.

### TestSDKCapture.html

单击Start启动签名捕获。
单击About以显示组件版本信息。
捕获签名后，单击信息以显示其上下文信息(谁/为什么/何时)。

### TestSDKCapture-SigText.html

捕获签名后，将显示SigText属性。
演示如何从保存的SigText恢复签名：
* 将SigText字符串复制到剪贴板
* 重新加载页面
* 将SigText字符串粘贴到SigText面板中
* 单击SetSigText


### TestSDKCapture-B64Image-Display.html

在这个版本中，调用RenderBitmap来生成一个png图像。
图像是在html img标记中设置的


### TestSDKCapture-Hash.html

在这个版本中，签名的哈希值是使用文本字段(First/Last Name)创建的。
验证将当前字段内容与签名中的哈希值进行比较。
如果字段内容更改，则验证失败。


### TestSDKCapture-Clipped.html

当与签名屏设备(如Intuos/DTU)一起使用时，笔形轨迹可以位于签名捕获窗口之外。
该示例演示了剪切掉捕获窗口外数据的效果。


### TestSDKWizardControl.html

演示如何使用向导控件进行签名捕获。

### WizardScript.html

演示如何使用向导控件进行签名捕获。

### Wizard-PIN-Demo.html

演示如何使用向导控件进行PIN代码输入。

### WizardScript-Image.html

演示如何使用图像代替按钮控件。


### WizardScript-Radio.html

演示如何使用单选按钮控件。


### WizardScript-TANDC-530.html

“条款和条件”页面演示了使用STU-530的彩色图像。



----
## Java Samples

要运行示例，必须首先安装Java开发工具包(JDK)。
此外，请确保在安装签名库时选择了Java组件:

![installer options](images/InstallerOptions.png)

Java组件与核心组件一起安装在
C:\Program Files (x86)\Common Files\WacomGSS

* flsx.jar
* flsx.dll


提供的批处理文件通过如下DOS命令提示符运行示例代码:

### 32-bit Java with Signature Library x86
启动DOS命令提示符并设置Java的路径，例如。
```
path="\Program Files (x86)\Java\jre1.8.0_181\bin"
```
使用提供的批处理文件运行示例，例如。
```
>Run-Java.bat CaptureImage.java
Compiling CaptureImage ...

Run CaptureImage.java ...
Created Signature image file: sig.png

>
```

### 64-bit Java with Signature Library x64
启动DOS命令提示符并设置Java的路径，例如。
```
PATH="\Program Files\Java\jdk1.8.0_31\bin"
```
使用提供的批处理文件运行示例，例如。
```
>Run-Java.x64.bat CaptureImage.java
Compiling CaptureImage ...

Run CaptureImage.java ...
Created Signature image file: sig.png

>
```

| 示例                        | 说明                                                                             |
| ----------------------------- | ----------------------------------------------------------------------------------------|
| CaptureImage.java             | 调用签名捕获，将签名呈现给 sig.png  |
| DecodeImage.java              | 读取sig.png，显示签名信息   |
| CaptureImageClipped.java      | 当与签名屏设备(如Intuos/DTU)一起使用时，笔迹可以位于签名捕获窗口之外。该示例演示了裁切掉在捕获窗口外数据的效果。 |
| CaptureImageRelative.java     | 演示签名的定位  |
| WizardScript.java             | 演示如何使用向导控件  |
| WizardScript_byteArray.java   | 创建签名图像的字节数组 |
| WizardUpload.java             | 将指定的图像上传到STU显示屏  |
| TestSigCapt                   | Eclipse 样式的项目签名程序 |
| TestWizSigCapt                | Eclipse 样式的项目签名捕获向导    |
| TestWizSigCaptSimulate        | Eclipse 样式的项目演示发送按钮事件  |



----
## C# Samples

Visual Studio项目包含在VS2010文件夹中。
这些项目包括对签名库中安装的互操作（intero）文件的引用。
当你运行安装程序时，一定要包含.NET组件：

![installer options](images/InstallerOptions.png)

互操作文件与库一起安装在 Program Files\Common Files\WacomGSS

打开 .sln 解决方案文件以打开项目，然后生成并运行。

| 示例                        | 说明                                                                             |
| ----------------------------- | ----------------------------------------------------------------------------------------|
| TestSigCapt                   | 调用签名捕获并显示签名 |
| TestWizSigCapt                | 使用向导控件捕获签名 |
| TestAXSigCapt                 | 演示如何在Windows窗体中使用ActiveX控件 |

----

## Visual Basic Samples
Visual Studio项目包含在VS2010VB文件夹中。
这些项目包括对签名库中安装的互操作文件的引用。
运行安装程序时，请确保包含c#示例中描述的.NET组件。

打开 .sln 解决方案文件以打开项目，然后生成并运行。

| 示例                        | 说明                                                                             |
| ----------------------------- | ----------------------------------------------------------------------------------------|
| TestSigCapt                   | 调用签名捕获并显示签名 |
| TestWizSigCapt                | 使用向导控件捕获签名 |


----
## C++ Samples

Visual Studio项目包含在CPP文件夹中。

打开 .sln 解决方案文件以打开项目，然后生成并运行。

| 示例                        | 说明                                                                             |
| ----------------------------- | ----------------------------------------------------------------------------------------|
| TestSigCaptCPP                | 调用签名捕获并显示签名 |
| TestWizSigCaptCPP             | 使用向导控件捕获签名 |

----
## Delphi Samples

Embarcadero Delphi项目包含在Delphi文件夹中。

打开项目文件以生成并运行示例。

| 示例                        | 说明                                                                             |
| ----------------------------- | ----------------------------------------------------------------------------------------|
| TestSigCapt                   | 调用签名捕获并显示签名 |
| TestSigCaptHash               | 调用签名捕获并演示Hash函数 |
| TestWizSigCapt                | 使用向导控件捕获签名 |

----
----




