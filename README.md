## 技术架构 ##
![Alt text](readme_static/frame.jpg)

### Wechat ###
我们在客户端上选择微信平台的小程序，因为它兼容性好且占用户资源少。
小程序的实现上传图片给服务器，接受并显示服务器回传的诊断报告。

### 云端　###
我们采用Azure提供的CVM(Cloud Virtual Machine)．系统版本是centos7.2。
我们的网络服务采用的nginx+django．django完成所有的网络功能架构部署．由于wechat的安全需要，我们需要nginx开启https协议。
我们的所有图片处理以python opencv为主，其提供了大量的操作工具。同时我们用pillow来生成报告

#### Region Of Interest ####
这一环节接受wechat端发送的手掌图片，将感兴趣的图片区域进行处理送到下一环节。
具体操作步骤包括：
* 手掌轮廓检测。将手掌与背景分离开， 我们采用肤色侦测的方法， 基于人皮肤和背景在YCbCr色彩空间差异大的特点来分离背景。
* 定锚。为了下一步的区域划分，必须要给出几个参考点。我们参考点选择的是4个指沟的位置。先用求的手掌的凸包，再求手掌轮廓中距离凸包距离最远的4个点，既是指沟。
* 区域划分。根据参考点的位置就可以划分区域。目的是一个区域尽可能只包含一条特征掌纹。

#### Feature Extract ####
这一环节接收多个区域图片，对每一个区域进行特征提取，


  

