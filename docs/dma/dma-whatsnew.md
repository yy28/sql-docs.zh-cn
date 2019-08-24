---
title: 数据迁移助手 (SQL Server) 中的新增功能 |Microsoft Docs
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 2a4780c9be50275959a0f32091b90c518ccea124
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000587"
---
# <a name="whats-new-in-data-migration-assistant"></a>数据迁移助手的新增功能
本文列出了每个版本的数据迁移助手 (DMA) 中的新增内容。

## <a name="dma-v45"></a>DMA 版本4。5

DMA 的5v 版本提供对将文件系统中托管的 SQL Server Integration Services (SSIS) 包迁移到 Azure SQL 数据库或 Azure SQL 数据库托管实例的评估支持。

## <a name="dma-v44"></a>DMA 4。4

用于 DMA 的 v2.0 版本支持将评估上载到 Azure Migrate。

## <a name="dma-v43"></a>DMA v4.3

DMA 的 v4.0 版本提供对以下内容的支持:

* 基于工作负荷评估的 Azure SQL 数据库托管实例的 SKU 建议。
* RDS SQL Server 作为评估的源。
* 作为目标的 Azure SQL 数据库托管实例的代理作业评估。
* 忽略某些评估规则的功能;dma 评估结果中将不会显示在 DMA 中配置的 "ignoreErrorCodes" 属性中指定的错误代码列表。
* 在作业活动步骤中评估 T-sql 查询并提供相应的建议
* 扩展事件评估 (公共预览版)。

此外, 此版本的 DMA 提高了在数据库中处理大量架构对象的性能, 并提供了与相关的 bug 修复:

* 在某些情况下, 用本机编译编译的过程。
* 复杂的数据库架构。

## <a name="dma-v42"></a>DMA v4.2

在从本地 SQL Server 迁移到 Azure SQL 数据库托管实例时, DMA 的4.2 版本为一个或多个服务器实例的目标准备情况评估提供命令行支持。 现在, 客户可以使用 DMA 命令行来收集有关其数据库架构的元数据、检测阻止程序, 并了解影响迁移到 Azure SQL 数据库托管实例的部分支持或不支持的功能。 然后, 可以使用提供的 Power BI 模板来呈现结果。

## <a name="dma-v41"></a>DMA v4.1

版本为4.1 的4.1 版本引入了对迁移到 Azure SQL 数据库托管实例的本地 SQL Server 数据库的全面评估的支持。

评估工作流可帮助检测以下问题, 这些问题可能会影响迁移到 Azure SQL 数据库托管实例:

* **支持的或部分支持的功能**。 DMA 会针对目标 Azure SQL 数据库托管实例部分支持或不支持的功能, 评估源 SQL Server 数据库中的功能。 然后, 该工具提供一组全面的建议、Azure 中可用的替代方法和缓解措施, 以便客户在计划迁移项目时可以将此信息纳入考虑。

* **兼容性问题**。 DMA 还识别与以下方面相关的兼容性问题:

  * 重大更改:可能破坏迁移到目标数据库的功能的特定架构对象。  建议在数据库迁移后修复这些架构对象。
  * 行为更改:报告的架构对象可能会继续工作, 但它们可能会表现出不同的行为, 例如性能下降。
  * 信息性问题:这些对象不会影响迁移, 但可能已不推荐使用功能 SQL Server 版本。

完成评估后, 请使用[Azure 数据库迁移服务](https://azure.microsoft.com/services/database-migration/)(DMS) 执行将 SQL Server 数据库迁移到 Azure SQL 数据库托管实例。  DMS 支持[脱机](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)(一次) 和[联机](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)(最小停机) 数据库迁移到 Azure SQL 数据库托管实例。

## <a name="dma-v40"></a>DMA v4.0

V2.0 的 v2.0 版本引入了 Azure SQL 数据库 SKU 建议功能, 该功能允许用户根据从承载数据库的计算机收集的性能计数器来识别最低建议的 Azure SQL 数据库 SKU。 此功能提供与定价层、计算级别和最大数据大小以及每月估计成本相关的建议。 它还提供将所有数据库批量预配到 Azure 的功能。

> [!NOTE]
> 当前只能通过命令行接口 (CLI) 使用此功能。

有关更多详细信息, 请参阅文章[为本地数据库标识正确的 AZURE SQL 数据库 SKU](dma-sku-recommend-sql-db.md)。

## <a name="dma-v36"></a>DMA v3.6

3\.6 版本的 DMA 为受最常见迁移阻止程序影响的架构对象引入了 "自动修复"。

此版本为以下迁移阻止程序和行为更改问题提供了 autofix:

* 使用未限定的联接语法的架构对象。
* 使用旧 RAISEERROR 语句的架构对象。
* 使用 Order By 整数文本的 SQL 语句。

DMA 为受列出的问题影响的对象执行自动架构转换, 并在继续进行架构转换之前提示用户进行确认。 用户可以查看建议的代码更改, 然后接受或拒绝任何给定数据库对象的所有转换。

DMA 使用 Microsoft 程序合成 (PROSE) 技术建议代码修补程序。 了解有关[PROSE](https://microsoft.github.io/prose/)的详细信息。

## <a name="dma-v35"></a>DMA v3.5

DMA 的3.5 版包含以下添加项:

* 迁移到 Azure SQL Database 的显著性能改进 (基准测试表明, 此过程比早期版本的 DMA 更快四倍)。
* 内存占用量经过进一步优化, 可以提高迁移工作流的稳定性。
* 在架构和数据迁移过程中跳过评估的功能 (如果在迁移之前已经执行了评估并解决了任何中断的架构对象)。
* 解决此问题的解决方法, 即, 当为备份文件提供了无效的网络共享路径时, 在将本地 SQL Server 本地版本升级到更高版本或在 Azure Vm 上 SQL Server 时, 该工具会崩溃。

## <a name="dma-v34"></a>DMA v3.4

7\.3 版本的 DMA 包含以下添加项:

* 支持 SQL Server 2017 作为迁移到 Azure SQL 数据库的源。
* 增强了稳定性、性能和评估规则的正确性。

## <a name="dma-v33"></a>DMA v3.3

使用适用于2017的 v2.0 版本, 可以在 Windows 和 Linux 上将本地 SQL Server 实例迁移到新版本的 SQL Server。 尽管适用于 Windows 和 Linux 的总体迁移工作流是相同的, 但对于 Linux 的 SQL Server 2017, 需要考虑几个额外的注意事项。

### <a name="specifying-the-back-up-path"></a>指定备份路径

Linux 和 Windows 使用不同的路径格式。 因此, 迁移到 Linux 上的 SQL Server 2017 要求用户同时提供 Windows 和 Linux 版本的路径到物理文件的位置。 您可以根据物理文件的位置, 以不同的方式提供两个版本的路径。
如果物理备份文件在运行的计算机上:

* Linux, 使用 "samba" 共享与网络上的其他计算机共享文件。
* Windows, 使用 "mnt" 命令将共享安装到运行 Linux 的计算机上。

> [!NOTE]
> 有关使用 "samba" 共享或 "mnt" 命令的详细信息超出了本文的讨论范围。

### <a name="migrating-windows-logins"></a>迁移 Windows 登录名

当 Linux 上的 SQL Server 2017 正式支持 Active Directory (AD) 登录名的迁移时, 它需要其他配置才能成功运行。 有关在 Linux 上的 SQL Server 2017 上设置 Active Directory 登录名的详细信息, 请参阅文章[Active Directory 身份验证 Linux 上的 SQL Server](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) 。 执行所需的配置后, 安装完成, 你可以像平常一样迁移 Active Directory 登录名。 标准的 SQL 身份验证按预期方式工作, 无需进行任何其他设置。

## <a name="dma-v32"></a>DMA v3.2

3\.2 版3.2 版包含以下添加项:

* 使用新的迁移工作流将架构和数据迁移从本地 SQL Server 数据库启用到 Azure SQL Database。
* 在将架构迁移到 Azure SQL 数据库的过程中, DMA 为源数据库对象编写脚本, 提供有关如何解决任何潜在的兼容性问题的指导, 然后将架构部署到 Azure。

## <a name="dma-v31"></a>DMA v3.1

用于 DMA 的3.1 版本包含以下添加项:

* 改进了对 Azure SQL 数据库的评估建议, 如数据库排序规则、使用不受支持的系统存储过程和 CLR 对象。
* 迁移到 Azure SQL 数据库时, 兼容性级别为130、120、110和100的评估指南。

## <a name="dma-v30"></a>DMA v3.0

的3.0 版 DMA 扩展了 Azure SQL 数据库评估, 以提供综合建议, 帮助解决与相关的问题:

* 迁移阻碍性问题。
* 部分或不受支持的功能和函数。

## <a name="dma-v21"></a>DMA v2.1

DMA 的2.1 版包含以下添加项:

* 用于在无人参与模式下运行评估的命令行支持, 有助于大规模运行评估。 有关更多详细信息, 请参阅文章[从命令行运行数据迁移助手](dma-commandline.md)。
* 用户启动和关闭 DMA 时的性能改进。
* 能够配置 SQL 连接超时。有关更多详细信息, 请参阅文章[数据迁移助手的配置设置](dma-configurationsettings.md)。

## <a name="dma-v20"></a>DMA v2.0

2\.0 版的 DMA 包含改进的 Stretch database 功能建议, 提供可最大程度地节省存储空间的正确优先级表。

## <a name="dma-v10"></a>DMA v1.0

DMA 1.0 版是初始版本, 它提供了:

* 发现可能影响升级到 SQL Server 本地版本的问题。 任何发现都被描述为兼容性问题, 并分为以下几个方面:
  * 重大更改
  * 行为更改
  * 已弃用的功能
* 发现目标 SQL Server 平台中的新功能, 数据库在升级后可从中受益。 任何发现均被描述为功能建议, 并分为以下几个方面:
  * 性能
  * 安全性
  * 存储
* 执行评估的新式用户体验。

## <a name="see-also"></a>请参阅

[数据迁移助手概述](../dma/dma-overview.md)
