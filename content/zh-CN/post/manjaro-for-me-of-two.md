+++
author = "roiwk"
title = "关于我选择Manjaro作为桌面系统 第二集 NVIDIA驱动"
date = "2022-09-03"
description = "关于我选择Manjaro作为桌面系统 第二集 NVIDIA驱动"
tags = [
    "Manjaro", "NVIDIA",
]
keywords = [
    "Manjaro", "NVIDIA",
]
categories = [
    "Manjaro", "NVIDIA",
]
draft = false
+++


# 关于我选择Manjaro作为桌面系统 第二集 NVIDIA驱动

>系统已安装，默认环境也都够用了，现在开始安装N卡驱动。  
>显卡放着,不能让它不干活啊，生产队的驴都不敢这么歇着。  

## 【推荐】方法一: 从Manjaro存储库自动安装Nvidia驱动
---

1. 自动检测系统，并安装适当的Nvidia驱动
   ```shell
   sudo mhwd -a pci nonfree 0300
   ```
2. 重启系统
   ```shell
   sudo reboot
   ```
3. 重启后，配置显卡
   ```shell
   nvidia-settings
   ```

  官方库有支持就是简单直接，一步到位。**安装成功**  

## 方法二: 使用官网驱动安装
---

[Nvidia官网搜索驱动下载][Nvidia官网搜索驱动]

具体安装步骤请参考这里 [^官网安装步骤]

[Nvidia官网搜索驱动]: https://www.nvidia.com/Download/index.aspx?lang=en-us
[^官网安装步骤]: https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-manjaro-linux

## 遇到的问题与解决:
---
1. 我的GTX1050Ti,推荐方法安装完成之后，默认没使用到显卡，驱动安装成功了。
   - 解决方案： 安装optimus-manager  
   - 配置与安装借鉴：  
      1. 双显卡切换情况，N卡和intel核卡[^借鉴1]  
      2. 显卡切换，整体安装与```/etc/ssdm.conf```配置过程，借鉴内容[^借鉴2]  
      3. ```optimus-mananer --switch nvidia```时，报错时，借鉴报错信息[^借鉴3]


[^借鉴1]: http://www.caotama.com/1153480.html
[^借鉴2]: https://archived.forum.manjaro.org/t/guide-install-and-configure-optimus-manager-for-hybrid-gpu-setups-intel-nvidia/92196
[^借鉴3]: https://github.com/Askannz/optimus-manager#important--manjaro-kde-users

## 总结
---
  推荐安装方式还是简单，安装之后，切换使用显卡，出现了问题，查了半天，  
  最终成功切换到N卡，附显卡监控图：
![GPU status](/images/manjaro-GPU-stats.png)