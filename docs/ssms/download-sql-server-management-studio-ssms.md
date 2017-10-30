---
title: "下载 SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 10/09/2017
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
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: be3d22491e1cf5e6446f9ac597d613e1d203a28e
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>下载 SQL Server Management Studio (SSMS)

SSMS 是一种集成环境，用于管理从 SQL Server 到 SQL 数据库的任何 SQL 基础结构。 SSMS 提供用于配置、监视和管理 SQL 实例的工具。 使用 SSMS 部署、监视和升级应用程序使用的数据层组件，以及生成查询和脚本。

使用 SQL Server Management Studio (SSMS) 在本地计算机或云端查询、设计和管理数据库和数据仓库，无论它们位于何处。

**SSMS 是免费的！**

SSMS 17.x 是最新一代的 SQL Server Management Studio，可支持 SQL Server 2017。

**[![download](../ssdt/media/download.png)下载 SQL Server Management Studio 17.3](https://go.microsoft.com/fwlink/?linkid=858904)**

**[![download](../ssdt/media/download.png)下载 SQL Server Management Studio 17.3 升级包（将 17.x 升级到 17.3）](https://go.microsoft.com/fwlink/?linkid=858906)**

SSMS 17.x 安装不会升级或替换 SSMS 16.x 或更早版本。 SSMS 17.x 与以前的版本并行安装，因此，这两个版本均可供使用。
如果计算机包含 SSMS 的并行安装，请验证你是否针对特定需求启动相应的版本。 最新版本标记为 Microsoft SQL Server Management Studio 17，并有一个新图标： 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> SQL Server PowerShell 模块现可通过 PowerShell 库单独安装。  有关详细信息，请参阅[下载说明](download-sql-server-ps-module.md)。

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**版本信息**

版本号：17.3

此版本的内部版本号为：14.0.17199.0

## <a name="new-in-this-release"></a>此版本中的新增功能

SSMS 17.3 是 SQL Server Management Studio 的最新版本。 SSMS 的 17.x 一代提供对 SQL Server 2008 到 SQL Server 2017 几乎所有功能领域的支持。 版本 17.x 也支持 SQL Analysis Service PaaS。

版本 17.3 包括：

- 新添加的“导入平面文件”向导通过智能框架简化了 CSV 文件的导入体验，极大地减少了所需的用户干预或领域的专业知识。 有关详细信息，请参阅[将平面文件导入到 SQL 向导](../relational-databases/import-export/import-flat-file-wizard.md)。
- “XEvent 探查器”节点已添加到对象资源管理器。 有关详细信息，请参阅[使用 SSMS XEvent 探查器](../relational-databases/extended-events/use-the-ssms-xe-profiler.md)。
- 更新了性能仪表板历史等待报表中的等待过滤和分类。
- 添加了“预测”函数的语法检查。
- 添加了外部库管理查询的语法检查。
- 添加了对外部库管理的 SMO 支持。
- 添加了对“已注册服务器”窗口的“启动 PowerShell”支持（需要新的 SQL PowerShell 模块）。
- AlwaysOn：已为可用性组添加[只读路由支持](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)。
- 添加了一个用于将跟踪详细信息发送到“Active Directory - 含 MFA 支持的通用身份验证”登录的输出窗口（默认为关闭状态；必须在“工具”>“选项”>“Azure 服务”>“Azure 云”>“ADAL 输出窗口跟踪级别”下的用户设置中开启）。 
- 查询存储： 
  - 即使 QDS 为关闭状态，只要 QDS 已记录任何数据，就可以访问查询存储 UI。
  - 查询存储 UI 现在会在所有现有报表中公开等待分类。 这会让客户解锁顶级等待查询等方案。
- 包含可选的脚本参数标头（默认为关闭状态；可在“工具”>“选项”>“SQL Server 对象资源管理器”>“脚本”>“包括脚本参数标头”下的用户设置中启用）- [连接项 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199)。
- 已删除“RC”商标。

有关更改的完整列表，请参阅 [SQL Server Management Studio - 更改日志 (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)。

有关用户数据收集的信息，请参阅 [SQL Server 隐私声明](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx)。

## <a name="supported-sql-offerings"></a>支持的 SQL 产品/服务

* 此版本的 SSMS 适用于所有[受支持 SQL Server 版本 (SQL Server 2008 - SQL Server 2017)](https://support.microsoft.com/lifecycle?C2=1044)，并且在最大程度上支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。
* 没有显式阻止 SQL Server 2000 或 SQL Server 2005，但某些功能可能无法正常工作。
* 此外，SSMS 17.x 可与 SSMS 16.x 或 SQL Server 2014 SSMS 及早期版本并行安装。

## <a name="supported-operating-systems"></a>受支持的操作系统
  
与最新可用的服务包一起使用时，此版本的 SSMS 支持以下 64 位平台：
- Windows 10（64 位）
- Windows 8.1（64 位）
- Windows 8（64 位）
- Windows 7 (SP1)（64 位）
- Windows Server 2016 *
- Windows Server 2012 R2（64 位）
- Windows Server 2012（64 位）
- Windows Server 2008 R2（64 位）

\*SSMS 17.X 基于 Windows Server 2016 之前发布的 Visual Studio 2015 独立 shell。 Microsoft 非常重视应用兼容性，确保已发布的应用程序能在 Windows 最新版本上继续运行。 若要尽量减少在 Windows Server 2016 上运行 SSMS 时出现的问题，请确保 SSMS 已应用所有最新更新。 如果遇到与 Windows Server 2016 版 SSMS 有关的任何问题，请联系支持人员。 支持团队将确定问题是与 SSMS、Visual Studio 还是与 Windows 兼容性相关。 然后，支持团队将问题交接给相应的团队进行进一步调查。

## <a name="ssms-installation-tips-and-issues"></a>SSMS 安装提示和问题

### <a name="minimize-installation-reboots"></a>尽量减少安装重启的次数

* 执行以下操作以降低 SSMS 安装程序在安装结束时需要重新启动的可能性：
  * 请确保运行的是最新版 Visual C++ 2013 Redistributable Package。 需要版本 12.00.40649.5（或更高版本）。 仅需要版本 x64。
  * 验证计算机上的 .NET Framework 版本是否为 4.6.1（或更高版本）。
  * 关闭计算机上打开的其他任何 Visual Studio 实例。
  * 请确保计算机上已安装所有最新 OS 更新。
  * 所提及的操作通常只需执行一次。 有几种情况需要在额外升级到 SSMS 的同一主版本期间重新启动。 对于次要升级，计算机上已安装 SSMS 的所有要求。

* 若要查看已知问题和解决方法的列表，请参阅 [SQL Server Management Studio 发行说明](../ssms/sql-server-management-studio-release-notes.md)

## <a name="available-languages"></a>可用语言

> [!NOTE]
> 如果安装在以下平台中，非英语本地化版本的 SSMS 需要 [KB 2862966 安全更新程序包](https://support.microsoft.com/en-us/kb/2862966)：Windows 8、Windows 7、Windows Server 2012 和 Windows Server 2008 R2。

此版本的 SSMS 可以安装在以下语言中：

SQL Server Management Studio 17.3：<br>
[中文（中国大陆）](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [中文（中国台湾）](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)

SQL Server Management Studio 17.3 升级包（将 17.x 升级到 17.3）：<br>
[中文（中国大陆）](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x804) | [中文（中国台湾）](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40a)

## <a name="release-notes"></a>发行说明

以下是此 17.3 版本的问题和限制：

**常规 SSMS**

- 对于使用含 MFA 的 UA 的 Azure AD 身份验证，不支持以下 SSMS 功能：
   - 对于 Azure AD 身份验证，不支持数据库引擎优化顾问；存在以下已知问题：向用户显示的错误消息“无法加载文件或程序集 Microsoft.IdentityModel.Clients.ActiveDirectory,…”较为隐蔽， 而非按预期显示“数据库引擎优化顾问不支持 Microsoft Azure SQL 数据库。 (DTAClient)”。
- 尝试在 DTA 中分析查询会导致发生错误：“对象必须实现 IConvertible。 (mscorlib)”。
- 回归的查询缺少对象资源管理器中报表的查询存储列表。
   - 解决方法：右键单击“查询存储”节点，然后选择“查看回归的查询”。

**Integration Services (IS)**

- 对于 Scale Out 中的包执行，[catalog].[event_messagea] 中的 [execution_path] 不正确。[execution_path] 以“\Package”开头，而不是以包可执行文件的对象名称开头。 在 SSMS 中查看包执行的概述报表时，执行概述中“执行路径”的链接不起作用。 解决方法是，在概述报表上单击“查看消息”，检查所有事件消息。



## <a name="previous-releases"></a>以前的版本

[旧版 SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>反馈

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 客户端工具论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 中提出问题或建议](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>另请参阅

- [教程：SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 文档](sql-server-management-studio-ssms.md)
- [其他更新程序和 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

