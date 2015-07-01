## 简介 ##

红杏是一个跨平台的透明化翻墙工具，旨在尽可能简化翻墙时的软件配置，以便使一些没有代理配置选项的软件（尤其是手机软件）也能顺利翻墙。

  * 红杏本身并不提供代理功能，它基于[GAppProxy](http://gappproxy.googlecode.com/)，所以你必须首先有一个GAppProxy的Fetch Server。可以[自己在Google App Engine上搭建](http://skydao.com/post/google-app-engine-to-do-with-personal-proxy-server-second-edition/)，也可以使用他人搭建好的。
  * 红杏只支持HTTP（即将支持HTTPS）协议，且不支持除80（及334）外的网站端口。

## 典型应用场景 ##

  * 无需设置代理，直接在浏览器中访问Twitter、YouTube。
  * 使用手机上不支持自定义API地址的Twitter客户端，如Twittix。
  * 使用YouTube官方客户端翻墙访问。

## 原理说明 ##

我们伟大的墙广泛的运用“DNS劫持”技术阻挡我们正常访问一些网站，受此启发，红杏正是将DNS劫持运用于翻墙事业，并与反向代理技术相结合，实现了透明化的HTTP代理。

通过一个本地的DNS代理将需要翻墙访问的域名解析为本地IP（127.0.0.1），再借助本地反向代理间接获取目标网站的内容。

红杏的DNS代理部分基于[SmartDNS](http://smartdns.googlecode.com/)实现，反向代理部分基于http://gappproxy.googlecode.com/ GAppProxy]实现，两者是独立工作并协同实现翻墙的。前者可以换用更为简单的hosts绑定机制，后者也可替换为其它反向代理实现（未来将发布一个PHP的版本）。

---

## 红杏 for S60v3/v5 0.2 alpha ##

### 版本说明 ###
  * 目前仅支持HTTP，暂不支持HTTPS
  * SmartDNS部分在手机端运行尚有问题（可工作于PC端），因此DNS解析部分采取hosts文件的方案
  * 由于HTTPS尚未实现，所以访问Twitter只能使用plaintext验证，不能使用Secure。Twitter手机版网站访问不受此影响。

### 安装步骤 ###
  * 首先下载[Python for S60 Runtime 2.0](https://garage.maemo.org/frs/download.php/7486/PythonForS60_2.0.0.tar.gz)，安装压缩包中 PythonForS60\PyS60Dependencies 下的 pips.sis、ssl.sis、stdioserver.sis 及 Python\_2.0.0.sis。
  * 然后下载并安装红杏 0.2 alpha版。（下载地址见本页右侧）
  * 下载hosts文件（下载地址见本页右侧），并复制到手机的C:\Private\10000882下。（此步骤需要已破解的S60手机）

### 使用步骤 ###
  * 在手机端启动红杏主程序“Red Apricot”
  * 选择接入点，填入你的GAppProxy Fetch Server地址及（可选的）GAppProxy本地代理
  * “选项”菜单 - “保存”，稍等片刻连接上网络后，会提示“Started”。注意：每次使用都需要支持保存，只有选返回将无法正常工作。（这个问题将在下个版本中修正）
  * 不要退出红杏的主程序，接下来切换到系统菜单，就可以打开浏览器访问Twitter、Facebook、YouTube，或使用这些服务的软件。
  * 使用完之后，切换到红杏主程序，退出即可。

### 补充说明 ###
当前的hosts文件中仅包含了Twitter、Facebook、YouTube的域，如需翻墙访问更多网站，请参照该文件的已有部分自行添加。