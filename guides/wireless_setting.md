# DC_WLAN(2.4GHz)/DC_WLAN(5GHz) 连接配置

注：此配置方法同样适用于DCITS_WLAN(2.4GHz)/DCITS_WLAN(5GHz)/DC_Mobile

### 创建配置文件

1. 网络和共享中心 -> 设置新的连接或网络 -> 手动连接到无线网络
2. 输入网络配置信息
   - 网络名： `DC_WLAN(5GHz) / DC_WLAN(2.4GHz)`
   - 安全类型：`WPA2 - 企业`
   - 下一步 -> 更改连接设置(H) -> 安全选项卡
     - 设置 - **取消勾选** “通过验证证书来验证服务器的身份(V)”
     - 高级设置 - 指定身份验证模式为：`用户身份验证`

### 配置过程图片

![wifi_01](/images/wifi_01.png)

![wifi_02](/images/wifi_02.png)

![wifi_03](/images/wifi_03.png)

![wifi_04](/images/wifi_04.png)



### 常见问题解决

1. 为何要给客户端安装DC Root CA的证书
	- 默认情况下PEAP(PEAP-EAP-MS-CHAPv2)要求客户端信任服务器的证书，公司目前使用自建的公钥基础结构(PKI) ,根证书为DC Root CA，Radius服务器使用的证书是由第一分支（DC Encrption DV CA - G1） 签发的。为使连接过程中尽可能少的出现告警信息，需要客户端信任该证书体系，目前已经将相关的证书文件通过组策略下发到域内
	- 域内正常的计算机在连接无线时验证服务器证书时，不会出现证书不受信的情况（仅限于windows平台），在此情况下，可以在不手动添加无线配置文件的情况下直接点击连接`DC_WLAN(5GHz/2.4GHz)`
2. windows提示无法连接到此网络
	- 如果是直接点击连接的无线，建议手动按照步骤添加一下配置文件(主要是去掉验证服务器证书)
	- 检查计算机是否正常接收到下发的证书(附2)
	- 检查密码是否有误
3. 更改密码之后无法连接到公司的无线
	- 改密码之后建议连接有线同步一下密码（连网之后注销，再重新使用新密码登陆）//锁定之后使用新密码解锁貌似也是可以的
4. MacOS或者iPhone等连接公司无线，突然之间无法连接（改没改密码都有可能出现此类情况）
	- 正常情况下macos或者iphone只需要在密码发生变更的时候重新输入新密码即可，个别情况下MacOS在送往radius认证的数据中用户名字段中会包含一个 `$` 符号，导致送过来的账号无法在系统中完成认证
	- **解决方法**：使用`ITCode@digitalchina.com`的方式输入用户名，然后输入密码认证即可

### 附1：

初次连接无线时，出现以下提示，请忽略并点击连接即可

![wifi_connect_win7](/images/wifi_connect_win7.png)

![wifi_connect_win10](/images/wifi_connect_win10.png)

![wifi-connect-iphone](/images/wifi_connect_iphone.png)



### 附2:

#### 验证根证书是否正常下发

在命令行中敲rsop，在打开的组策略结果集中依次点开：`计算机设置`-`windows设置`-`安全设置`-`公钥策略` 检查受信任的根证书颁发机构和中级证书颁发机构中证书是否正常（需要包含`DC Root CA`和`DC Root CA 2020`)

如果电脑域关系正常，可通过`gpupdate /force` 更新组策略，获取推送的证书文件



#### 证书文件+无线配置文件路径：

> \\\\ishare\集团共享文件夹\DC Root CA\

手动安装证书的方法：双击`DC RootCA.crt/dc-rootca-2020.crt`，选择“安装证书”依次选择`存储位置：本地计算机`-`将所有的证书都放入下列存储，浏览选择"受信任的根证书颁发机构"` 点击完成随后将`dvg1_ca.crt`、`dc-entca.crt`、`ovg2_ca.crt`依次安装到计算机（cross证书选择安装），选择存储位置为本地计算机之后，直接点击下一步即可。

无线配置文件使用方法：

> netsh wlan add profile filename="dcwlan-5G.xml"
>
> netsh wlan add profile filename="dcwlan-24G.xml"



