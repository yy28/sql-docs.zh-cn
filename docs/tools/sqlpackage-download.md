---
title: 下载并安装 sqlpackage |Microsoft Docs
description: 下载并安装适用于 Windows、macOS 或 Linux 的 sqlpackage
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
ms.openlocfilehash: f966de4951e5c90dac8d6e48f00f8de6ff067e3c
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2019
ms.locfileid: "73033011"
---
# <a name="download-and-install-sqlpackage"></a>下载并安装 sqlpackage

sqlpackage 在 Windows、macOS 和 Linux 上运行。

下载并安装最新的 .NET Framework 版本以及 macOS 和 Linux 预览版：

|平台|下载|发布日期|版本|生成
|:---|:---|:---|:---|:---|
|Windows （x64）|[MSI 安装程序](https://go.microsoft.com/fwlink/?linkid=2108813)|2019 年 10 月 29 日|18.4|15.0.4573.2|
|macOS .NET Core （x64）|[zip 文件](https://go.microsoft.com/fwlink/?linkid=2108815)|2019 年 10 月 29 日| 18.4|15.0.4573.2|
|Linux .NET Core （x64） |[zip 文件](https://go.microsoft.com/fwlink/?linkid=2108814)|2019 年 10 月 29 日| 18.4|15.0.4573.2|
|Windows .NET Core （x64） |[zip 文件](https://go.microsoft.com/fwlink/?linkid=2109019)|2019 年 10 月 29 日| 18.4|15.0.4573.2|

有关最新版本的详细信息，请参阅[发行说明](release-notes-sqlpackage.md)。 若要下载其他语言，请参阅[可用语言](#available-languages)部分。

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>获取适用于 Windows 的 sqlpackage

此版本的 sqlpackage 包括标准 Windows 安装程序体验和 .zip： 

1. 下载并运行[适用于 Windows 的 DacFramework.msi 安装程序](https://go.microsoft.com/fwlink/?linkid=2108813)。
2. 打开一个新的命令提示符窗口，并运行 sqlpackage.exe
    - sqlpackage 会安装到 ```C:\Program Files\Microsoft SQL Server\150\DAC\bin``` 文件夹

## <a name="get-sqlpackage-net-core-for-windows"></a>获取适用于 Windows 的 sqlpackage .NET Core

1. 下载[适用于 Windows 的 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2109019)。
2. 若要提取文件，请在 Windows 资源管理器中右键单击该文件，然后选择 "全部提取 ..."，然后选择目标目录。
3. 打开新的终端窗口和 cd，到提取 sqlpackage 的位置：

   ```cmd
   > sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-macos"></a>获取 macOS 的 sqlpackage .NET Core

1. 下载[适用于 macOS 的 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2108815)。
2. 若要提取文件并启动 sqlpackage，请打开一个新的终端窗口并键入以下命令：

   ```bash
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   $ echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   $ source ~/.bash_profile
   $ sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-linux"></a>获取用于 Linux 的 sqlpackage .NET Core

1. 通过使用安装程序之一或 tar.gz 存档来下载[适用于 Linux 的 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2108814)：
2. 若要提取文件并启动 sqlpackage，请打开一个新的终端窗口并键入以下命令：

   ```bash
   cd ~
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   $ echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   $ chmod a+x ~/sqlpackage/sqlpackage
   $ source ~/.bashrc
   $ sqlpackage
   ```

   > [!NOTE]
   > 在 Debian、Redhat 和 Ubuntu 上，可能缺少依赖项。 使用以下命令安装这些依赖项，具体取决于你的 Linux 版本：

   **Debian：**

   ```bash
   $ sudo apt-get install libunwind8
   ```

   **Redhat：**

   ```bash
   $ yum install libunwind
   $ yum install libicu
   ```

   **Ubuntu：**

   ```bash
   $ sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   $ sudo apt-get install libicu52      # for 14.x
   $ sudo apt-get install libicu55      # for 16.x
   $ sudo apt-get install libicu57      # for 17.x
   $ sudo apt-get install libicu60      # for 18.x
   ```

## <a name="uninstall-sqlpackage-preview"></a>安装 sqlpackage（预览版）

如果使用 Windows 安装程序安装了 sqlpackage，则按照删除任何 Windows 应用程序的方式进行卸载。

如果使用 .zip 或其他存档安装了 sqlpackage，则删除文件。

## <a name="supported-operating-systems"></a>支持的操作系统

sqlpackage 在 Windows、macOS 和 Linux 上运行，并在以下平台上受支持：

### <a name="windows"></a>Windows

- Windows 10
- Windows 8.1
- Windows 7 SP1
- Windows Server 2008 R2
- Windows Server 2012 R2
- Windows Server 2016

### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="available-languages"></a>可用语言

可采用以下语言安装此版本的 sqlpackage：

sqlpackage Windows：  
[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x40a)

sqlpackage .NET Core Windows：  
[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x40a)

sqlpackage .NET Core macOS：  
[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x40a)

sqlpackage .NET Core Linux：  
[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x40a)

## <a name="next-steps"></a>Next Steps

- 了解有关 [sqlpackage](sqlpackage.md) 的详细信息

[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkId=521839)
