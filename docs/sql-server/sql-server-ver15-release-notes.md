---
title: SQL Server 2019 发行说明 | Microsoft Docs
ms.date: 03/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 6336e6ebc549d1be2787bb8a100efec1ea9b6836
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492849"
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

## <a name="ctp-24"></a>CTP 2.4
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的最新公开版本。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3 仅作为评估版提供。 不提供任何其他版本。 安装介质随附的 `license_Eval.rtf` 中描述了对 CTP 版本的支持。

可在以下其中一个位置找到有限的支持：

- 论坛
  - [SQL Server 反馈](https://aka.ms/sqlfeedback)
  - [SQL Server 入门](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 文档](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 或使用 [#sqlhelp](https://twitter.com/search?q=%23sqlhelp) 发布推文 [@SQLServer](https://twitter.com/SQLServer)

### <a name="documentation-ctp-24"></a>文档 (CTP 2.4)

- **问题及其对客户的影响**：SQL Server 2019 (15.x) 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 文档集中。 文章中特定于 SQL Server 2019 (15.x) 的内容通过“适用于”进行标注。

- 问题和对客户的影响：可按版本筛选 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文档。 使用每个文档页左上角的控件来筛选你的要求。

- **问题及其对客户的影响**：SQL Server 2019 (15.x) 没有可用的脱机内容。

### <a name="hardware-and-software-requirements-ctp-24"></a>硬件和软件要求 (CTP 2.4)

- **问题及其对客户的影响**：硬件和软件要求仍在审核中，还不是产品发布的最终版本。

  - **硬件**
    - [Windows - 处理器、内存和操作系统要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 系统要求](../linux/sql-server-linux-setup.md#system)
  - **软件**
    - Windows Server 2016 或更高版本。 有关其他要求，请参阅[安装 SQL Server 的要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2。 可从[下载中心](https://www.microsoft.com/download/details.aspx?id=53344)获取。
    - 对于 Linux，请参阅 [Linux - 受支持的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="updated-compiler"></a>更新后的编译器

- **问题及其对客户的影响**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 是通过更新后的编译器构建的。 CTP 2.1 具有一项已知问题，即浮点和其他转换方案的结果可能因更新后的编译器而返回与先前版本不同的值。 CTP 2.2 内附可确保受影响的方案与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 先前版本返回相同结果的任务。 自 CTP 2.3 版本起，已解决所有历史问题。 请将与 [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] 比较得出的所有结果异常立即报告给 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 团队](http://aka.ms/sqlfeedback)。

- **解决方法**：N/A

- **适用对象**：SQL Server 2019 CTP 2.4、CTP 2.3、CTP 2.2 和 CTP 2.1

### <a name="utf-8-collations"></a>UTF-8 排序规则

- **问题及其对客户的影响**：支持 UTF-8 的排序规则不能与其他一些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能一起使用。 如果正在使用以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能，则不支持 UTF-8：

  - 链接服务器
  - 内存中 OLTP
  - Polybase 外部表
  - 始终加密

  > [!Note]
  > 目前没有 UI 支持在 Azure Data Studio 或 SQL Server Data Tools (SSDT) 中选择支持 UTF-8 的排序规则。 最新的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] SSMS 版本支持在 UI 中选择支持 UTF-8 的排序规则。
 
- **解决方法**：没有针对 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 的解决方法。

- **适用对象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4、CTP 2.3、CTP 2.2、CTP 2.1 和 CTP 2.0。

### <a name="sql-graph"></a>SQL 图形

- **问题及其对客户的影响**：依赖于 DacFx 的工具（如导入-导出）不适用于新的图形功能：边缘约束或合并 DML。 在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中编写的脚本可能无法正常工作。

- **解决方法**：编写 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本并使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 SQLCMD 将能针对服务器运行这些脚本。 无法导出或导入创建边缘约束、具有新的合并 DML 语法或在图形对象上创建派生表/视图的数据库对象。 用户必须使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本在其数据库中手动创建此类对象。 

- **适用对象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4、CTP 2.3、CTP 2.2、CTP 2.1 和 2.0。

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全 Enclave 的 Always Encrypted

- **问题及其对客户的影响**：富计算正在等待多项性能优化，包括有限的功能（无索引等），并且当前默认处于禁用状态。

- **解决方法**：若要启用富计算，请运行 `DBCC traceon(127,-1)`。 有关详细信息，请参阅[启用富计算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

- **适用对象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4、CTP 2.3、2.2、CTP 2.1 和 2.0。

### <a name="system-dynamic-management-views"></a>系统动态管理视图

- **问题及其对客户的影响**：系统表值函数 [sys.dm_db_objects_disabled_on_compatibility_level_change](../relational-databases/system-dynamic-management-views/spatial-data-sys-dm-db-objects-disabled-on-compatibility-level-change.md) 返回 `dependency` 列中的随机值。

- **适用对象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4、CTP 2.3。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
