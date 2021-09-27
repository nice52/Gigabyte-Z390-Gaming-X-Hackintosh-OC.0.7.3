# Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3
![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/%E7%B3%BB%E7%BB%9F%E4%BF%A1%E6%81%AF.png)
## **1、硬件配置**
| 类型 | 型号 | 
| :------: | :------: |
| CPU | I7 8700K  | 
| 主板 | 技嘉Z390 Gaming X | 
| bios | F10i | 
| 显卡 | RX590 | 
| 内存 | 幻光戟3000 16GB*2 | 
| 无线网卡、蓝牙 | 黑苹果BCM943602CS | 
| 固态 | 英特尔760P 512G | 
| 电源 | 海盗船RM650 | 
| 机箱 | 乔思伯U5（前脸USB3.0*2个） | 
<br>


## **2、准备工作**
### 2.1  Bios设置
| **关闭以下选项** | **打开以下选项** | 
| :------: | :------: |
| Fast Boot  快速启动 | X.M.P 开启内存XMP，一般选profile 1 |
| secure boot 安全启动 | Above 4G decoding |
| CSM  | Hyper-Threading |
| VT-d | USB---EHCI/XHCI Hand-off |
| SGX | intel graphics （IGPU monitor），要选enable |
| Intel Platform Trust |    |


### 2.2  替换自己定制的三码
  **用GenSMBIOS-master软件生成三码，填入config文件，步骤简述如下：<br>**
（1)打开“GenSMBIOS.bat”软件，按提示回车进入功能菜单；键入"3"，回车；输入"iMac19,1"，回车，三码生成完毕，先不要关闭此窗口。过程如下图：<br>
![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/%E4%B8%89%E7%A0%81%E6%9B%BF%E6%8D%A2/%E5%9B%BE%E7%89%871.png)
![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/%E4%B8%89%E7%A0%81%E6%9B%BF%E6%8D%A2/%E5%9B%BE%E7%89%872.png)
![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/%E4%B8%89%E7%A0%81%E6%9B%BF%E6%8D%A2/%E5%9B%BE%E7%89%873.png)

(2)打开“ProperTree.bat”软件，加载“EFI/OC/config.plist”配置文件。定位到PlatformInfo → Generic ，将上面生成的三码填入配置文件对应的参数：
| 三码 | config.plist | 
| :------: | :------: |
| Serial | SystemSerialNumber  | 
| Board Serial | MLB | 
| UUID | SystemUUID | 

![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/%E4%B8%89%E7%A0%81%E6%9B%BF%E6%8D%A2/%E5%9B%BE%E7%89%875.png)<br>
填完后保存，不要关闭<br>
### 2.3  调整启动参数（针对Navi核心显卡，非Navi请无视）
定位到NVRAM  →  Add   →   7C436110-AB2A-4BBB-A880-FE41995C9F82   →   boot-args，加一条参数“agdpmod=pikera”。<br>
![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/%E4%B8%89%E7%A0%81%E6%9B%BF%E6%8D%A2/%E5%9B%BE%E7%89%874.png)

保存后退出，此时EFI文件为完全体，可以直接食用了。<br>
## **3、几点说明**
### 3.1    U盘定制情况
由于Mac OS限制USB端口最多15个（同一物理接口的USB2.0和3.0记作2个），因此有所取舍，并非所有的USB接口都同时支持3.0和2.0，具体如下表：
| 位置 | USB3.0 | USB2.0 |
| :------: | :------: | :------: |
| 机箱面板*2 | √ | √  |
| A-B | × | √  |
| C-D | √ | √  |
| E-H | √ | ×  |
<br>

![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/USB%E5%AE%9A%E5%88%B6.jpg)
<br>

### 3.2    硬件加速
<br>
在BIOS设置正确的情况下，核显可以直接驱动，硬件加速可以正常工作（用VideoProc测试通过）<br>

![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/%E7%A1%AC%E4%BB%B6%E5%8A%A0%E9%80%9F.png)

![image](https://github.com/nice52/Gigabyte-Z390-Gaming-X-Hackintosh-OC.0.7.3/blob/master/screenshot/%E6%98%BE%E5%8D%A1%E4%BF%A1%E6%81%AF.png)


## **4、安装过程-极简**
<br>
(1)下载镜像<br>
网上的集成opencore的原版镜像都可以，这里随便放一个不用充钱的https://macx.top/21288.html/comment-page-1<br>
(2)烧录启动盘<br>
用balenaEtcher软件将下载好的固件烧录进U盘（不小于16GB）<br>
(3)写入引导EFI<br>
用DiskGenius打开U盘的OC引导的ESP分区，使用“浏览文件”功能删掉固件自带EFI文件，然后将刚才调整好的EFI文件放进去
(4)系统安装<br>
重启按F12进启动菜单，选择OC对应的EUFI启动项，等待出现OC启动界面，选择安装MAC，之后按照提示安装苹果系统（不细说，具体百度）。
<br>

## **尾巴**
<br>

**前后折腾两三个礼拜，目前各项日常功能基本正常，声卡、网卡、显卡、核显都能正常驱动，应用商店能正常登陆和安装软件；休眠没试过（目前没发现异常），iMessage没试过（没有其他apple设备）暂未发现明显BUG。**
