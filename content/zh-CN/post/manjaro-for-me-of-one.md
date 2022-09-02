+++
author = "roiwk"
title = "关于我选择Manjaro作为我的桌面系统 第一集"
date = "2022-08-31"
description = "关于我选择Manjaro作为我的桌面系统 第一集"
tags = [
    "Manjaro", "Plasma Desktop",
]
keywords = [
    "Manjaro",
    "Plasma Desktop",
    "primer",
]
categories = [
    "Manjaro",
    "primer",
]
draft = false
+++


# 关于我选择Manjaro作为我的桌面系统 第一集

## 起因

---

***总的来说就是：还没钱买新电脑，这个还能用，想再折腾折腾***

- 手上笔记本,C盘**满了又删，删了又满**，基本每过两月就得经历；  
*CC cleaner* 安装了两年了；每次清理都有种上大学时用的手机的感觉，也是存储不够，天天满，天天清； 
- 用了5年多的笔记本，

  > win10-专业版  
  > 24G(16G+8G)  
  > 128G-SSD  
  > 1T-HHD  
  > I5-7th 4核  
  > GTX-1050Ti(4G显存)  

原配是8G，后面内存条降价时候加了个16G。（咔～，快照留念。）  

<details>
  <summary>
      <u>已安装的开发环境max 👇：</u>
  </summary>
docker,wsl,rust,php,golang,node,python,vscode,navicate,mobaxterm,postman,chrome,apifox,vnode
</details>
<br/>
所以，新系统必须具备我开发环境，GUI用着舒服就行。  
游戏的话，以后台式机打吧，这显卡，大游戏也支撑不了了，卡而且散热是个问题。  

## 开搞
---

去 [Distrowatch](https://distrowatch.com) 看了下，之前就关注过[Manjaro](https://manjaro.org/),排名还是在前5的,[Distrowatch-Manjaro](https://distrowatch.com/table.php?distribution=manjaro),果断准备用ta了。

- Manjaro 吸引我的优点：
桌面系统种类丰富-gnome,plasma,xface等；
稳定性-linux内核稳定版本；
官方软件库相对完整-有软件需求的，基本官方库就有了；

目标确定，开始操作：  

1. 下载镜像 [Manjaro官网下载](https://manjaro.org/download/)  
   - 我选了plasma kde桌面版（喜欢kde）。
2. 安装系统
   - 我使用了[Ventory](https://www.ventoy.net/cn/index.html)
   - 系统安装步骤，刚开始配个语言，认识`language`单词即可，选中文，全程鼠标操作，顺利完成。
   - *记住设置的密码和超级密码*
3. 安装软件
   - 启动后的系统，有`Manjaro Hello`软件会自动启动,  
  ![manjaro-hello](/images/manjaro-hello.png)  
  按需安装软件；这里都是推荐的，兼容性相对较高的软件。
  


## 还不错
---

- 快捷键操作，基本与win差不多,常用的都还能用，不喜欢的可以配置，`系统设置` 里可以设置；
  - <kbd>Win</kbd>+<kbd>E</kbd>
  - <kbd>Alt</kbd>+<kbd>Tab</kbd>
  - <kbd>Ctl</kbd>+<kbd>C</kbd>
  - <kbd>Ctl</kbd>+<kbd>V</kbd>
  - ...  

- win平台各种软件的替代方案：
  |win软件|manjaro软件|
  |:---|:---|
  |vscode|code-oss(vscode-linux版)|
  |chrome浏览器|chromium|
  |office|onlyoffice|
  |中文输入法|IBus [^IBus] |  

  `Manjaro Hello`->`Applications` 这个官方推荐app里，有许多常用软件，基本可以满足日常的工作所需。  

## 结束
---
 至此，基本的linux桌面版系统-**Manjaro**环境以有了，接下来继续熟悉和持续使用中～～

捣鼓半天设置的桌面：
![manjaro-hello](/images/Desktop-screenshot1.png)
 


[^IBus]: 打开`Manjaro Hello`->`Applications`->`Extended language support`->`Manjaro Asian Input Support Ibus` 选中，然后点击右上角`UPADATE SYSTEM`，安装并配置即可。