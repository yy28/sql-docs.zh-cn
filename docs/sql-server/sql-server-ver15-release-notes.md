---
title: SQL Server 2019 发行说明 | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2018
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology:
- server-general
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: e7c4447ce03c25eab91e62c03540906d29714d7f
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419093"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 预览版发行说明

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 社区技术预览 (CTP) 版本的限制和已知问题。 若要了解相关信息，请参阅：
- [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> 提供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 预览版以便体验即将发布版本的功能。 不支持或不许可将其用于生产。 不显式支持以下方案：
>
> - 与其他版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 并行安装
> - 卸载
> - 从 SQL Server 早期版本升级

试用 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]！
- [![从评估中心下载](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=862101) [下载 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 以在 Windows 上安装](http://go.microsoft.com/fwlink/?LinkID=862101)
- 在 Linux 上针对 [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md) 安装。
- [在 Docker 上运行 SQL Server 2019](../linux/quickstart-install-connect-docker.md)。

## <a name="ctp-20-september-2018"></a>CTP 2.0（2018 年 9 月）

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的首个公开发行版。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 仅作为评估版提供。 不提供任何其他版本。 安装介质随附的 license_Eval.rtf 中描述了对 CTP 2.0 的支持。

可在以下其中一个位置找到有限的支持：

- 论坛
  - [SQL Server 反馈](http://aka.ms/sqlfeedback)
  - [SQL Server 入门](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 文档](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 或使用 [#sqlhelp](https://twitter.com/search?q=%23sqlhelp) 发布推文 [@SQLServer](http://twitter.com/SQLServer)

### <a name="documentation-ctp-20"></a>文档 (CTP 2.0)

- 问题和对客户的影响：SQL Server 2019 (15.x) 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 文档集中。 文章中特定于 SQL Server 2019 (15.x) 的内容通过“适用于”进行标注。

- 问题和对客户的影响：可按版本筛选 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文档。 使用每个文档页左上角的控件来筛选你的要求。 

- 问题及对客户的影响：SQL Server 2019 (15.x) 没有可用的脱机内容。

### <a name="hardware-and-software-requirements"></a>硬件和软件要求

- 问题和对客户的影响：硬件和软件要求仍在审核中，还不是产品发布的最终版本。

  - **硬件**
    - [Windows - 处理器、内存和操作系统要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 系统要求](../linux/sql-server-linux-setup.md#system)
  - **软件**
    - Windows Server 2016 或更高版本。 有关其他要求，请参阅[安装 SQL Server 的要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - 对于 Linux，请参阅 [Linux - 受支持的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="sql-graph"></a>SQL 图形

问题和对客户的影响：依赖于 DacFx 的工具（如导入-导出）不适用于新的图形功能 - 边缘约束或合并 DML。 在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中编写的脚本可能无法正常工作。

解决方法：编写 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本并使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 SQLCMD 将能针对服务器运行这些脚本。 无法导出或导入创建边缘约束、具有新的合并 DML 语法或在图形对象上创建派生表/视图的数据库对象。 用户必须使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本在其数据库中手动创建此类对象。 

适用于：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

### <a name="utf-8-collations"></a>UTF-8 排序规则

问题和对客户的影响：支持 UTF-8 的排序规则不能与其他一些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能一起使用。 如果正在使用以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能，则不支持 UTF-8：

- SQL Server 复制
- 链接服务器
- 内存中 OLTP
- Polybase 外部表

  另请注意，目前没有 UI 支持在 Azure Data Studio 或 SSDT 中选择支持 UTF-8 的排序规则。 最新的 SSMS 版本支持在 UI 中选择支持 UTF-8 的排序规则。

解决方法：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 没有解决方法。

适用于：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

### <a name="lightweight-query-profiling-infrastructure"></a>轻型查询分析基础结构

问题及对客户的影响：执行命令 `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = ON` 会返回一个语法错误。 任何依赖于执行此命令的方案都将失败。

> [!NOTE]
> 目前，轻型查询分析基础结构 (LWP) 无法在单个数据库级别进行控制，并且在默认情况下为所有数据库保持启用状态。 有关 LWP 的详细信息，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

解决方法：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 没有解决方法。

适用于：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全 Enclave 的 Always Encrypted

问题和对客户的影响：富计算正在等待多项性能优化，包括有限的功能（无索引等），并且当前默认处于禁用状态。

解决方法：若要启用富计算，请运行 `DBCC traceon(127,-1)`。 有关详细信息，请参阅[启用富计算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

适用于：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

### <a name="sql-server-integration-services-ssis-transfer-database-task"></a>SQL Server Integration Services (SSIS) 传输数据库任务

问题和对客户的影响：当 `Transfer Database Task` 配置为在 `Database Online` 模式下传输数据库时，它可能会失败并显示以下错误：

>任务上的 Execute 方法返回了错误代码 0x80131500（传输数据时出错。 有关详细信息，请参阅内部异常。） Execute 方法必须成功，并使用 "out" 参数指示该结果。

解决方法：在服务器上执行 `DBCC TRACEON (7416,-1)`，然后重试。

### <a name="sql-server-machine-learning-services-installation-failure"></a>SQL Server 机器学习服务安装失败

问题/对客户的影响：在主域具有信任关系问题的计算机上安装 SQL Server 机器学习服务失败。 在这种情况下，日志中将显示以下错误：
 
>  错误：0 : System.SystemException：此工作站与主域之间的信任关系在 System.Security.Principal.NTAccount.TranslateToSids(IdentityReferenceCollection sourceAccounts, Boolean& someFailed) 中失败...

在位于以下位置的日志中进行验证：

* `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.log`
* `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\rxLibs\RegisterRExt.log`
解决方法：解决域信任问题并重试安装。

适用于：SQL Server 2019 CTP 2.0。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
