---
title: "下载 SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
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
ms.translationtype: HT
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: a689293fadb1a442f94d88cc06a9e7a4ef06650f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/08/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>下载 SQL Server Management Studio (SSMS)

SSMS 是一种集成环境，用于管理从 SQL Server 到 SQL 数据库的任何 SQL 基础结构。 SSMS 提供用于配置、监视和管理 SQL 实例的工具。 使用 SSMS 部署、监视和升级应用程序使用的数据层组件，以及生成查询和脚本。

使用 SQL Server Management Studio (SSMS) 在本地计算机或云端查询、设计和管理数据库和数据仓库，无论它们位于何处。

**SSMS 是免费的！**

SSMS 17.x 是最新一代的 SQL Server Management Studio，可支持 SQL Server 2017。

**[![下载](../ssdt/media/download.png)下载 SQL Server Management Studio 17.2](https://go.microsoft.com/fwlink/?linkid=854085)**

**[![下载](../ssdt/media/download.png)下载 SQL Server Management Studio 17.2 升级包（将 17.x 升级到 17.2）](https://go.microsoft.com/fwlink/?linkid=854087)**

SSMS 17.x 安装不会升级或替换 SSMS 16.x 或更早版本。 SSMS 17.x 与以前的版本并行安装，因此，这两个版本均可供使用。
如果计算机包含 SSMS 的并行安装，请验证你是否针对特定需求启动相应的版本。 最新版本标记为 Microsoft SQL Server Management Studio 17，并有一个新图标： 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> SQL Server PowerShell 模块现可通过 PowerShell 库单独安装。  有关详细信息，请参阅[下载说明](download-sql-server-ps-module.md)。

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**版本信息**

版本号：17.2 此版本的内部版本号为：14.0.17177.0

## <a name="new-in-this-release"></a>此版本中的新增功能

SSMS 17.2 是 SQL Server Management Studio 的最新版本。 SSMS 的 17.x 一代提供对 SQL Server 2008 到 SQL Server 2017 几乎所有功能领域的支持。 版本 17.x 也支持 SQL Analysis Service PaaS。

版本 17.2 包括：

- 多重身份验证 (MFA)
  - 用于含多重身份验证的通用身份验证的多用户 Azure AD 身份验证（具有 MFA 的 UA）
  - 为含 MFA 的通用身份验证添加了新的用户凭据输入字段，以支持多用户身份验证。
- 连接对话框现在支持以下 5 种身份验证方法：
  - Windows 身份验证
  - SQL Server 身份验证
  - Active Directory - 含 MFA 支持的通用身份验证
  - Active Directory - 密码
  - Active Directory - 集成

- DacFx 向导的数据库导入/导出现在可以使用含 MFA 的通用身份认证。
- 有关 API 支持，请参阅 [IUniversalAuthProvider 接口](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)。
- 具有 MFA 的 Azure AD 通用身份验证使用的 ADAL 托管库已升级到 3.13.9 版本。
- 新 CLI 界面，支持用于 SQL 数据库和 SQL 数据仓库的 Azure AD 管理设置。

 有关 Active Directory 身份验证方法的详细信息，请参阅[使用 SQL 数据库和 SQL 数据仓库进行通用身份验证（MFA 的 SSMS 支持）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)和[配置 SQL Server Management Studio 的 Azure SQL 数据库多重身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)。

- 输出窗口具有在对象资源管理器节点扩展期间运行的查询条目
- 为 Azure SQL 数据库启用了查看设计器
- SSMS 中的对象资源管理器脚本对象的默认脚本选项已更改：
  - 以前，新安装的默认值是将生成的脚本面向最新版本的 SQL Server（当前为 SQL Server 2017）。
  - 在 SSMS 17.2 中，添加了一个新选项：将脚本设置与源进行匹配。 当设置为 True 时，生成的脚本面向与要从其中脚本化对象的服务器相同的版本、引擎类型和引擎版本。
  - 默认情况下，“将脚本设置与源进行匹配”值设置为 True，因此新安装的 SSMS 将自动默认始终将对象脚本化到与原始服务器相同的目标。
  - 当“将脚本设置与源进行匹配”设置为 False 时，正常的脚本目标选项将被启用，并像以前那样运行。
  - 此外，所有脚本选项已移动到其各自的部分 - 版本选项。 它们不再位于“常规脚本选项”下。

- 在“从 URL 还原”中增加了对国家云的支持
- QueryStoreUI 报表现在支持来自 sys.query_store_runtime_stats 的其他指标（RowCount、DOP、CLR Time 等）。
- Azure SQL 数据库现在支持 IntelliSense
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- 安全性：连接对话框将默认不信任服务器证书，并为 Azure SQL 数据库连接请求加密
- 对 Linux 上的 SQL Server 支持的常规改进：
 - 重新使用数据库邮件节点
 - 解决了一些与路径相关的问题
 - 改进了活动监视器稳定性
 - “连接属性”对话框显示正确的平台
- 现在可将性能仪表板服务器报表用作默认报表：
  - 可连接到 SQL Server 2008 和更新版本。
  - 缺失索引子报表使用计分来帮助确定最有用的索引。
  - 历史等待统计信息子报表现在将等待聚合为类别。 默认情况下，将筛选出空闲和睡眠等待。
  - 新的历史闩锁子报表。
- Showplan 节点搜索允许在计划属性中进行搜索。 轻松查找任何操作符属性，如表名。 在查看计划时使用此选项：
  - 右键单击计划，并在上下文菜单中单击“查找节点”选项
  - 使用 Ctrl+F

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

SQL Server Management Studio 17.2：<br>
[中文（中国大陆）](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [中文（中国台湾）](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

SQL Server Management Studio 17.2 升级包（将 17.x 升级到 17.2）：<br>
[中文（中国大陆）](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x804) | [中文（中国台湾）](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40a)

## <a name="release-notes"></a>发行说明

以下是此 17.2 版本的问题和限制：

- 使用“Active Directory - 含 MFA 支持的通用身份验证”身份验证的查询窗口在打开约一小时或更长时间后尝试执行查询时可能会遇到类似以下错误：

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of *ConnectRetryCount* to increase the number of recovery attempts.`

   重新运行查询应忽略错误并成功。

- 对于使用含 MFA 的通用身份验证的 Azure AD，不支持以下 SSMS 功能：
  - “新建表/视图”设计器显示旧式登录提示，并且不适用于 Azure AD 身份验证。
  - “编辑前 200 行”功能不支持 Azure AD 身份验证。
  - “已注册的服务器”组件不支持 Azure AD 身份验证。
  - “数据库引擎优化顾问”不支持 Azure AD 身份验证。 存在以下已知问题：向用户显示的错误消息“无法加载文件或程序集 Microsoft.IdentityModel.Clients.ActiveDirectory”无用， 而不是显示“数据库引擎优化顾问不支持 Microsoft Azure SQL 数据库 (DTAClient)”。

**AS**

- SSAS 中的对象资源管理器将不会在 AS Azure 连接属性中显示 Windows 身份验证用户名。
有关详细信息，请参阅 [SSMS 更改日志](sql-server-management-studio-changelog-ssms.md)。

## <a name="previous-releases"></a>以前的版本

[旧版 SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>反馈

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 客户端工具论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 中提出问题或建议](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>另请参阅

- [教程：SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 文档](sql-server-management-studio-ssms.md)
- [其他更新程序和 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

