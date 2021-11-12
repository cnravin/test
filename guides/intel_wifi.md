### 部分英特尔无线网卡无法搜索到WiFi6 AP广播SSID的解决办法

​		根据intel官方描述，部分802.11ac的网卡发现并连接到WiFi6(802.11ax) AP广播的SSID上，无法正常使用无线网络，intel推荐以下网卡的用户更新无线网卡驱动以解决问题。

> 注：请先确认网卡型号（可参考末尾附1），再寻找下载驱动文件，22.10.0版本仅包含驱动文件，不含PROSet组件

#### Windows 10 

- > [WiFi_22.10.0_Driver64_Win10.zip][WiFi_22.10.0_Driver64_Win10.zip]

  其他下载选项：

  - 32位系统驱动

    [WiFi_22.10.0_Driver32_Win10.zip][WiFi_22.10.0_Driver32_Win10.zip]

  支持的网卡适配器如下：

  ```
  Intel® Wireless-AC 9560
  Intel® Wireless-AC 9462
  Intel® Wireless-AC 9461
  Intel® Wireless-AC 9260
  Intel® Dual Band Wireless-AC 8265
  Intel® Dual Band Wireless-AC 8260
  ```

  

- > [WiFi_22.10.0_Driver64_Win10.zip][WiFi_22.10.0_Driver64_Win10.zip]

  其他下载选项：

  - 32位系统驱动

    [WiFi_22.10.0_Driver32_Win10.zip][WiFi_22.10.0_Driver32_Win10.zip]

  支持的网卡适配器型号如下：

  ```
  Intel® Dual Band Wireless-AC 3168
  Intel® Wireless 7265 Family (Rev.D)
  Intel® Dual Band Wireless-AC 3165
  ```

  

- > [3160-7260-7265C_WiFi_21.10.1_PROSet64_Win.exe][3160-7260-7265C_WiFi_21.10.1_PROSet64_Win.exe]

  其他下载选项：

  - 32位系统驱动
  
    [3160-7260-7265C_WiFi_21.10.1_PROSet32_Win.exe][3160-7260-7265C_WiFi_21.10.1_PROSet32_Win.exe]
  
  支持的网卡适配器型号如下：
  
  ```
  Intel® Wireless 7265 Family (Rev.C)
  Intel® Wireless 7260 Family
  Intel® Dual Band Wireless-AC 3160
  ```



#### Windows7

- > [WiFi_21.40.5_PROSet64_Win7.exe][WiFi_21.40.5_PROSet64_Win7.exe]

  其他下载选项：

  - 32位系统驱动

    [WiFi_21.40.5_PROSet32_Win7.exe][WiFi_21.40.5_PROSet32_Win7.exe]

  - 仅驱动程序，不含PROSet组件

    x86：[WiFi_21.40.5_Driver32_Win7.zip][WiFi_21.40.5_Driver32_Win7.zip]

    x64：[WiFi_21.40.5_Driver64_Win7.zip][WiFi_21.40.5_Driver64_Win7.zip]

  支持的网卡适配器型号如下：

  ```
  Intel® Dual Band Wireless-AC 8265
  Intel® Dual Band Wireless-AC 8260
  Intel® Dual Band Wireless-AC 3168
  Intel® Wireless 7265 Family (Rev.D)
  Intel® Dual Band Wireless-AC 3165
  ```

- > [3160-7260-7265C_WiFi_21.10.1_PROSet64_Win.exe][3160-7260-7265C_WiFi_21.10.1_PROSet64_Win.exe]

  其他下载选项：

  - 32位系统驱动
  
    [3160-7260-7265C_WiFi_21.10.1_PROSet32_Win.exe][3160-7260-7265C_WiFi_21.10.1_PROSet32_Win.exe]
  
  支持的网卡适配器型号如下：

  ```
  Intel® Wireless 7265 Family (Rev.C)
  Intel® Wireless 7260 Family
  Intel® Dual Band Wireless-AC 3160
  ```
  



#### 附1：如何安装非可执行程序的驱动程序文件

1. 先确认网卡是什么型号的，然后根据系统版本下载对应的驱动文件

   - 命令行查看方法

     通过cmd-->`netsh wlan show interface` (命令提示符中输入该命令)

   ```
   PS C:\Users\ccg> netsh wlan show interface
   
   系统上有 1 个接口:
   
       名称                   : WLAN
       描述                   : Intel(R) Dual Band Wireless-AC 3165	<---------据此可确定网卡的型号信息
       GUID                   : 828dda06-e46a-4700-876c-1ade7776687c
       物理地址               : 00:dc:dc:cc:e5:d5
       状态                   : 已连接
       SSID                   : DC_WLAN(5GHz)
       BSSID                  : cc:46:d6:ad:71:4f
       网络类型               : 结构
       无线电类型             : 802.11ac
       身份验证               : WPA2 - 企业
       密码                   : CCMP
       连接模式               : 自动连接
       信道                   : 44
       接收速率(Mbps)         : 200
       传输速率 (Mbps)        : 200
       信号                   : 99%
       配置文件               : DC_WLAN(5GHz)
   
       承载网络状态  : 不可用
   
   PS C:\Users\ccg>
   ```

   - 图形界面查看方法：

     在`计算机/此电脑` 上右击 选择`管理`然后再打开的窗口中选择`设备管理器`-`网络适配器` 然后查找`Intel xxxx Wireless xxxx`的网卡，根据最后的数字可判断网卡型号（也可通过命令行直接敲`devmgmt.msc`打开设备管理器）

   ![devmgmt.png](/images/devmgmt.png)

2. 手动安装驱动程序

   将下载好的驱动程序`zip包`解压，然后在网卡上右击选择`更新驱动程序`--`浏览我的电脑以查找驱动程序` 然后在弹出的窗口中浏览选择解压文件所在的目录，然后确认一路下一步完成即可。

   如果是可执行的exe程序，直接双击运行即可。安装向导完成之后重启计算机即可完成驱动更新。

#### 附2：

- Intel 关于802.11ac网卡驱动问题说明

  https://www.intel.cn/content/www/cn/zh/support/articles/000054799/network-and-i-o/wireless.html

- intel官方驱动下载链接（请先参考文件支持型号）

  https://downloadcenter.intel.com/zh-cn/download/30056/-IT-PROSet



[3160-7260-7265C_WiFi_21.10.1_PROSet32_Win.exe]:https://it.digitalchina.com/resource/intel-wifi-drivers/3160-7260-7265C_WiFi_21.10.1_PROSet32_Win.exe
[3160-7260-7265C_WiFi_21.10.1_PROSet64_Win.exe]:https://it.digitalchina.com/resource/intel-wifi-drivers/3160-7260-7265C_WiFi_21.10.1_PROSet64_Win.exe
[WiFi_21.40.5_Driver32_Win7.zip]:https://it.digitalchina.com/resource/intel-wifi-drivers/WiFi_21.40.5_Driver32_Win7.zip
[WiFi_21.40.5_Driver64_Win7.zip]:https://it.digitalchina.com/resource/intel-wifi-drivers/WiFi_21.40.5_Driver64_Win7.zip
[WiFi_21.40.5_PROSet32_Win7.exe]:https://it.digitalchina.com/resource/intel-wifi-drivers/WiFi_21.40.5_PROSet32_Win7.exe
[WiFi_21.40.5_PROSet64_Win7.exe]:https://it.digitalchina.com/resource/intel-wifi-drivers/WiFi_21.40.5_PROSet64_Win7.exe
[WiFi_22.10.0_Driver32_Win10.zip]:https://it.digitalchina.com/resource/intel-wifi-drivers/WiFi_22.10.0_Driver32_Win10.zip
[WiFi_22.10.0_Driver64_Win10.zip]:https://it.digitalchina.com/resource/intel-wifi-drivers/WiFi_22.10.0_Driver64_Win10.zip	"."
