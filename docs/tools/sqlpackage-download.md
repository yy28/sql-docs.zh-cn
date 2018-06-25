---
title: 下载并安装 sqlpackage |Microsoft 文档
description: 下载并安装针对 Windows、 macOS 或 Linux 的 sqlpackage
ms.custom: tools|sos
ms.date: 06/18/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 4e5528ca046de83385171890fbda389928e41cf3
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703828"
---
# <a name="download-and-install-sqlpackage"></a>下载并安装 sqlpackage

sqlpackage 在 Windows、 macOS 和 Linux 上运行。

下载并安装最新的.NET Framework 版本和 macOS 及 Linux 预览版：

|平台|下载|发布日期|版本|生成|
|:---|:---|:---|:---|:---|
|Windows|[安装程序](https://go.microsoft.com/fwlink/?linkid=875508)|2018 年 1 月 25 日|17.4.1|14.0.3917.1|
|macOS（预览版）|[.zip](https://go.microsoft.com/fwlink/?linkid=873927)|2018 年 5 月 9 日 |0.0.1|15.0.4057.1|
|Linux（预览版）|[.zip](https://go.microsoft.com/fwlink/?linkid=873926)|2018 年 5 月 9 日 |0.0.1|15.0.4057.1|

## <a name="get-sqlpackage-for-windows"></a>获取 Windows sqlpackage

此版本的 sqlpackage 包括标准的 Windows 安装程序体验和.zip: 

**安装程序**

1. 下载并运行[DacFramework.msi 面向 Windows 的安装程序](https://go.microsoft.com/fwlink/?linkid=875508)。
2. 打开一个新的命令提示符窗口，并运行 sqlpackage.exe
    - sqlpackage 安装到```C:\Program Files\Microsoft SQL Server\140\DAC\bin```文件夹

## <a name="get-sqlpackage-preview-for-macos"></a>获取 macOS sqlpackage （预览版）

1. 下载[macOS 的 sqlpackage](https://go.microsoft.com/fwlink/?linkid=873927)。
2. 若要提取的文件并启动 sqlpackage，打开一个新的终端窗口并键入以下命令：

   **.zip 安装：**
   ```bash 
   mv ~/Downloads/sqlpackage-linux-<version string> ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage 
   ``` 

## <a name="get-sqlpackage-preview-for-linux"></a>获取适用于 Linux 的 sqlpackage （预览版）

1. 下载[适用于 Linux 的 sqlpackage](https://go.microsoft.com/fwlink/?linkid=873926)使用安装程序或 tar.gz 存档之一：
2. 若要提取的文件并启动 sqlpackage，打开一个新的终端窗口并键入以下命令：

   **.zip 安装：**
   ```bash 
   cd ~ 
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bashrc
   source ~/.bashrc 
   sqlpackage 
   ``` 

   > [!NOTE]
   > 在 Debian、 Redhat 和 Ubuntu，您可能必须缺失的依赖关系。 使用以下命令安装这些依赖项，具体取决于你的 Linux 版本：
   

   **Debian:** 
   ```bash
   sudo apt-get install libuwind8
   ```

   **Redhat：** 
   ```bash
   yum install libunwind 
   yum install libicu 
   ```

   **Ubuntu：** 
   ```bash
   sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   sudo apt-get install libicu52      # for 14.x
   sudo apt-get install libicu55      # for 16.x
   sudo apt-get install libicu57      # for 17.x
   sudo apt-get install libicu60      # for 18.x
   ```


## <a name="uninstall-sqlpackage-preview"></a>卸载 sqlpackage （预览版）

如果你安装 sqlpackage 使用 Windows installer，然后卸载相同的方式删除所有 Windows 应用程序。

如果使用.zip 或其他存档安装 sqlpackage，只需删除的文件。

## <a name="supported-operating-systems"></a>支持的操作系统

sqlpackage 在 Windows、 macOS 和 Linux 上运行，并且支持以下平台上：

### <a name="windows"></a>Windows
- Windows 10
- Windows 8.1 
- Windows 8 
- Windows 7 SP1 
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012 
- Windows Server 2008 R2

### <a name="macos"></a>macOS
- macOS 10.13 高 Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- 详细了解[sqlpackage](sqlpackage.md)

[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkId=521839)
