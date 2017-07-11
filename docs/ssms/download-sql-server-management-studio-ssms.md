---
title: "下载 SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安装 SSMS，下载 SSMS，最新的 SSMS"
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- "SQL Management Studio 安装"
- "下载 SQL Management Studio"
- MS SQL Management Studio
- "安装 SQL Management Studio"
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 60bdb820d74be98dd051d4729463d375d2a5202a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/03/2017

---
<a id="download-sql-server-management-studio-ssms" class="xliff"></a>

# 下载 SQL Server Management Studio (SSMS)
SQL Server Management Studio (SSMS) 是一种集成环境，用于管理从 SQL Server 到 SQL 数据库的任何 SQL 基础结构。 SSMS 提供用于配置、监视和管理你在任何地方部署的 SQL 实例的工具。 用户可以通过 SSMS 部署、监视和升级应用程序使用的数据层组件，以及生成查询和脚本。 

此版本改进了与以前版本的 SQL Server 的兼容性、具有独立 Web 安装程序以及新版本可用时 SSMS 内部的 Toast 通知。  
  
![下载](../ssdt/media/download.png)免费 SSMS！ **[下载 SQL Server Management Studio 17.1](https://go.microsoft.com/fwlink/?linkid=849819)**  SSMS 17.X 是最新一代的 SQL Server Management Studio，可支持 SQL Server 2017。 

![下载](../ssdt/media/download.png) [下载 SQL Server Management Studio 17.1 升级包（将 17.0 升级到 17.1）](https://go.microsoft.com/fwlink/?linkid=849821)

> [!NOTE]
> SQL Server PowerShell 模块现可通过 PowerShell 库单独安装。  有关详细信息，请参阅[下载说明](download-sql-server-ps-module.md)。

<a id="sql-server-management-studio" class="xliff"></a>

## SQL Server Management Studio   
**版本信息**  
  
版本号：17.1  
此版本的内部版本号为：14.0.17119.0

<a id="new-in-this-release" class="xliff"></a>

## 此版本中的新增功能  

SSMS 17.1 是对 SQL Server Management Studio 的 17.X 一代的首次更新。  17.X 一代提供对 SQL Server 2008 到 SQL Server 2017 几乎所有功能领域的支持。  版本 17.X 也是支持 SQL Analysis Service PaaS 的一代 SSMS。

版本 17.1 包括：

* 对若干用户报告问题的修复 
* 新的 Integration Services Scale-out 管理工具

有关更改的完整列表，请参阅   
                [SQL Server Management Studio (SSMS) - 更改日志](../ssms/sql-server-management-studio-changelog-ssms.md)  
   
有关用户数据收集的信息，请参阅   
                [SQL Server 隐私声明](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx) 
  
<a id="supported-sql-offerings" class="xliff"></a>

## 支持的 SQL 产品/服务
  
* 此版本的 SSMS 适用于所有[受支持 SQL Server 版本 (SQL Server 2008 - SQL Server 2017)](https://support.microsoft.com/en-us/lifecycle?C2=1044)，并且在最大程度上支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。  
* 没有显式阻止 SQL Server 2000 或 SQL Server 2005，但某些功能可能无法正常工作。  
* 此外，SSMS 17.X 可与 SSMS 16.X 或 SQL Server 2014 SSMS 及早期版本并行安装。 
  
<a id="supported-operating-systems" class="xliff"></a>

## 受支持的操作系统
  
此版本的 SSMS 在与最新可用的 Service Pack 一起使用时支持以下平台：   
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7 (SP1)
- Windows Server 2016
- Windows Server 2012（64 位） 
- Windows Server 2012 R2（64 位） 
- Windows Server 2008 R2（64 位）  

>[!NOTE]
>SSMS 17.X 基于 Windows Server 2016 之前发布的 Visual Studio 2015 独立 shell。 Microsoft 非常重视应用兼容性，确保已发布的应用程序能在 Windows 最新版本上继续运行。 若要尽量减少运行 SSMS Windows Server 2016 时出现的问题，请确保 SSMS 已应用所有最新更新。 如果遇到与 Windows Server 2016 版 SSMS 有关的任何问题，请联系支持人员。 支持人员将确定是关于 SSMS、Visual Studio 的问题还是关于 Windows 兼容性的问题，然后将问题重定向到相应团队。

<a id="ssms-installation-tips-and-issues" class="xliff"></a>

## SSMS 安装提示和问题
**尽量减少安装重新启动的次数**

- 执行以下操作以降低 SSMS 安装程序在安装结束时需要重新启动的可能性：
  - 请确保运行的是最新版 Visual C++ 2013 Redistributable Package。 需要版本 12.00.40649.5（或更高版本）。 仅需要版本 x64。
  - 验证计算机上的 .NET Framework 版本是否为 4.6.1（或更高版本）。
  - 关闭计算机上打开的其他任何 Visual Studio 实例。
  - 请确保计算机上已安装所有最新 OS 更新。
  - 通常一次只需一个指示的操作。 有几种情况需要在额外升级到 SSMS 的同一主版本期间重新启动。 对于次要升级，计算机上已安装 SSMS 的所有要求。

- 若要查看已知问题和解决方法的列表，请参阅 [SQL Server Management Studio 发行说明](../ssms/sql-server-management-studio-release-notes.md)

<a id="available-languages" class="xliff"></a>

## 可用语言  
> 如果安装在以下平台中，非英语本地化版本的 SSMS 需要 [KB 2862966 安全更新程序包](https://support.microsoft.com/en-us/kb/2862966)：Windows 8、Windows 7、Windows Server 2012 和 Windows Server 2008 R2。 
  
此版本的 SSMS 可以安装在以下语言中：

SQL Server Management Studio 17.1：<br>
[中文（中华人民共和国）](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

SQL Server Management Studio 17.1 升级包（将 17.0 升级到 17.1）：<br>
[中文（中华人民共和国）](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40a)

<a id="previous-releases" class="xliff"></a>

## 以前的版本  
[旧版 SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  
  
<a id="feedback" class="xliff"></a>

## 反馈  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 客户端工具论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 中提出问题或建议](https://connect.microsoft.com/SQLServer/Feedback)  
  
<a id="see-also" class="xliff"></a>

## 另请参阅  
[教程：SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 文档](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[其他更新程序和 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



