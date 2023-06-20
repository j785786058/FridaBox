# 脱离PC在Android上运行Frida脚本及发送HTTP请求
## 一、脱离PC在Android上运行Frida脚本
## 步骤1：frida-server
要使用Frida，首先需要将frida-server拷贝到Android设备的/data/local/tmp目录,可以在 [frida-server](https://github.com/frida/frida/releases) 下载
## 步骤2：开机自动运行frida-server
正常情况下/data/local/tmp/frida-server就可以启动frida服务，如果想开机自动启动frida，需要下载 [MagiskFrida](https://github.com/AeonLucid/MagiskFrida) 压缩包放到Magisk插件
## 步骤3：安装DroidFrida
DroidFrida已经集成好了frida-inject，可以在Android设备直接注入JS脚本 [DroidFrida](https://github.com/ac3ss0r/DroidFrida)
## 步骤4：frida-inject
下载[frida-inject](https://github.com/frida/frida/releases) 并改名为frida64，上传到Android设备的/data/local/tmp目录， **注意版本号要对应**


## 二、Frida脚本主动发起Http请求
## 步骤1：AndroidAsync
下载 [AndroidAsync](https://github.com/koush/AndroidAsync)，把jar包打包为dex文件，放到/data/local/tmp
## 步骤2：调用dex发起请求
在脚本中调用 androidAsync.dex 发起请求
``` 
Java.openClassFile("/data/local/tmp/androidAsync.dex").load();
var AsyncHttpClient = Java.use("com.koushikdutta.async.http.AsyncHttpClient");
var url = "http://xxx.com;
AsyncHttpClient.getDefaultInstance().execute(url,null);	
```
