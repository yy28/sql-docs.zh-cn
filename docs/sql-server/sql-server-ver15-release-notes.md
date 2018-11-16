---
title: SQL Server 2019 发行说明 | Microsoft Docs
ms.date: 11/06/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 2c21ac917845b8162348b93fec3b868f1f748592
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703855"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 预览版发行说明

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 社区技术预览 (CTP) 版本的限制和已知问题。 若要了解相关信息，请参阅：
- [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> 提供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 预览版以便体验即将发布版本的功能。 不支持或不许可将其用于生产。 不显式支持以下方案：
>
> - 与其他版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 并行安装
> - 从任意版本升级现有的 SQL Server 实例

试用 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]！
- [![从评估中心下载](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [下载 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 以在 Windows 上安装](https://go.microsoft.com/fwlink/?LinkID=862101)
- 在 Linux 上针对 [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md) 安装。
- [在 Docker 上运行 SQL Server 2019](../linux/quickstart-install-connect-docker.md)。

## <a name="ctp-21-november-2018"></a>CTP 2.1（2018 年 11 月）
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的最新公开发行版。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 仅作为评估版提供。 不提供任何其他版本。 安装介质随附的 license_Eval.rtf 中描述了对 CTP 2.1 的支持。

可在以下其中一个位置找到有限的支持：

- 论坛
  - [SQL Server 反馈](https://aka.ms/sqlfeedback)
  - [SQL Server 入门](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 文档](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 或使用 [#sqlhelp](https://twitter.com/search?q=%23sqlhelp) 发布推文 [@SQLServer](https://twitter.com/SQLServer)

### <a name="documentation-ctp-21"></a>文档 (CTP 2.1)

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
    - Microsoft .NET Framework 4.6.2。 可从[下载中心](https://www.microsoft.com/download/details.aspx?id=53344)获取。
    - 对于 Linux，请参阅 [Linux - 受支持的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="floating-point-results"></a>浮点结果

- **问题及对客户的影响**：SQL Server 2019 预览版使用已更新的编译器来生成 SQL Server。 在某些情况下，使用新编译器编译的代码可能返回与旧版 SQL Server 不同的浮点数值。 在未来 CTP 中，行为变更将仅限于新兼容性级别 (150)。

- **解决方法**：不适用

- **适用于**：SQL Server 2019 CTP 2.1

### <a name="sql-server-integration-services-ssis-page-deployment-after-switching-db-to-single-user-mode-and-then-switching-back"></a>将 DB 切换到单用户模式然后再切换回来后的 SQL Server Integration Services (SSIS) 页面部署

- **问题及对客户的影响**：SSISB 从单用户模式切换回多用户模式后，部署包时可能会报告以下错误：

  `Cannot continue the execution because the session is in the kill state.`

- **解决方法**：停止并重启 SQL Server 实例，并将 SSISDB 切换回多用户模式。 

- **适用于**：SQL Server 2019 预览版 CTP 2.1


### <a name="udf-inlining"></a>UDF 内联 

- **问题及对客户的影响**：在一些极端情况下，对用户定义函数内联的嵌套调用无法正确验证安全性。
  
- **解决方法**：使用 `INLINE = OFF` 设置禁用此类 UDF 的 UDF 内联。

- **适用于**：SQL Server 2019 CTP 2.1

### <a name="lightweight-query-profiling-infrastructure"></a>轻型查询分析基础结构

- 问题及对客户的影响：执行命令 `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = ON` 会返回一个语法错误。 任何依赖于执行此命令的方案都将失败。

  > [!NOTE]
  > 目前，轻型查询分析基础结构 (LWP) 无法在单个数据库级别进行控制，并且在默认情况下为所有数据库保持启用状态。 有关 LWP 的详细信息，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

- **解决方法**：没有针对 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 的解决方法。

- **适用于**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 和 CTP 2.0。

### <a name="utf-8-collations"></a>UTF-8 排序规则

- 问题和对客户的影响：支持 UTF-8 的排序规则不能与其他一些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能一起使用。 如果正在使用以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能，则不支持 UTF-8：

  - SQL Server 复制
  - 链接服务器
  - 内存中 OLTP
  - Polybase 外部表

    另请注意，目前没有 UI 支持在 Azure Data Studio 或 SSDT 中选择支持 UTF-8 的排序规则。 最新的 SSMS 版本支持在 UI 中选择支持 UTF-8 的排序规则。

- **解决方法**：没有针对 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 的解决方法。

- **适用于**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 和 CTP 2.0。

### <a name="sql-graph"></a>SQL 图形

- **问题及对客户的影响**：依赖于 DacFx 的工具（如导入-导出）不适用于新的图形功能：边缘约束或合并 DML。 在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中编写的脚本可能无法正常工作。

- 解决方法：编写 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本并使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 SQLCMD 将能针对服务器运行这些脚本。 无法导出或导入创建边缘约束、具有新的合并 DML 语法或在图形对象上创建派生表/视图的数据库对象。 用户必须使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本在其数据库中手动创建此类对象。 

- **适用于**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 和 2.0。

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全 Enclave 的 Always Encrypted

- **问题及对客户的影响**：富计算正在等待多项性能优化，包括有限的功能（无索引等），并且当前默认处于禁用状态。

- 解决方法：若要启用富计算，请运行 `DBCC traceon(127,-1)`。 有关详细信息，请参阅[启用富计算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

- **适用于**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 和 2.0。

### <a name="sql-server-integration-service---fuzzy-lookup-transformation"></a>SQL Server Integration Service - 模糊查找转换

- **问题/对客户的影响**：如果将模糊查找转换设置为重用索引，则模糊查找转换将失败并显示以下错误：

  `The specified delimiters do not match the delimiters used to build the pre-existing match index "...". This error occurs when the delimiters used to tokenize fields do not match. This can have unknown effects on the matching behavior or results.`

- **解决方法**：不适用

- **更多信息**：不适用  

- **适用于**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]CTP2.1

## <a name="ctp-20-september-2018"></a>CTP 2.0（2018 年 9 月）

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的首个公开发行版。

### <a name="sql-server-integration-services-ssis-transfer-database-task"></a>SQL Server Integration Services (SSIS) 传输数据库任务

- 问题和对客户的影响：当 `Transfer Database Task` 配置为在 `Database Online` 模式下传输数据库时，它可能会失败并显示以下错误：

  >任务上的 Execute 方法返回了错误代码 0x80131500（传输数据时出错。 有关详细信息，请参阅内部异常。） Execute 方法必须成功，并使用 "out" 参数指示该结果。

- 解决方法：在服务器上执行 `DBCC TRACEON (7416,-1)`，然后重试。

- 适用于：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
