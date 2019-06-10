---
title: 什么是数据迁移助手 (SQL Server) 中的新增功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/18/2019
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
manager: jroth
ms.openlocfilehash: f88562c25982ce8c5d6c8d4b87dd629e4ba57c03
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794309"
---
# <a name="whats-new-in-data-migration-assistant"></a>数据迁移助手的新增功能
本文列出了每个版本中添加的数据迁移助手 (DMA)。

## <a name="dma-v43"></a>DMA v4.3

DMA v4.3 版本提供以下支持：

* SKU 建议为 Azure SQL 数据库托管实例的工作负荷评估为基础。
* RDS SQL Server 作为源进行评估。
* 代理作业评估为 Azure SQL 数据库托管实例为目标。
* 能够忽略某些评估规则;DMA 评估结果中不会显示在 DMA 中配置的 ignoreErrorCodes 属性中指定的错误代码的列表。
* 在作业活动步骤并提供相应建议的 T-SQL 查询的评估
* 扩展的事件评估 （公共预览版）。

此外，此版本的 DMA 提供了用于处理大量的数据库，以及与相关的 bug 修复中的架构对象提高的性能：

* 与本机编译，在某些情况下编译的过程。
* 复杂的数据库架构。

## <a name="dma-v42"></a>DMA v4.2

从本地 SQL Server 迁移到 Azure SQL 数据库托管实例时，DMA 的 4.2 版版本为目标准备情况评估一个或多个服务器实例提供命令行支持。 客户现在可以使用 DMA 命令行来收集有关其数据库架构的元数据，检测阻塞程序，并了解会影响迁移到 Azure SQL 数据库托管实例的部分支持或不受支持的功能。 然后可以使用提供的 Power BI 模板呈现结果。

## <a name="dma-v41"></a>DMA v4.1

DMA 4.1 版版本引入了对在本地 SQL Server 数据库迁移到 Azure SQL 数据库托管实例的综合评估的支持。

评估工作流可帮助你检测可能会影响迁移到 Azure SQL 数据库托管实例的以下问题：

* **不受支持或部分支持的功能**。 DMA 评估使用的部分支持或在目标 Azure SQL 数据库托管实例上不受支持的功能的源 SQL Server 数据库。 然后，该工具提供了一系列全面的建议，在 Azure 中，并缓解步骤，以便客户可以考虑此信息规划其迁移项目时可用的替代方法。

* **兼容性问题**。 DMA 还标识与相关的以下几个方面的兼容性问题：

  * 重大更改：可能会中断迁移到目标数据库的功能特定的架构对象。  我们建议在数据库迁移后修复这些架构对象。
  * 行为更改：报告的架构对象可能会继续运行，但它们可能会表现出不同的行为，例如性能下降。
  * 信息性问题：这些对象不会影响迁移，但可能已弃用的功能的 SQL Server 版本。

评估完成后，使用我们[Azure 数据库迁移服务](https://azure.microsoft.com/services/database-migration/)(DMS) 来执行迁移到 Azure SQL 数据库托管实例将 SQL Server 数据库。  同时支持 DMS[脱机](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)（一次性） 和[联机](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)（最小停机时间） 数据库迁移到 Azure SQL 数据库托管实例。

## <a name="dma-v40"></a>DMA v4.0

DMA v4.0 版本引入了 Azure SQL 数据库 SKU 的建议功能，它使用户能够确定建议基于从托管数据库的计算机收集性能计数器的 Azure SQL 数据库 SKU 的最小。 此功能提供了与定价层、 计算级别和最大数据大小，以及每月预计的成本相关的建议。 它还提供预配所有数据库到 Azure 中大容量的能力。

> [!NOTE]
> 此功能当前处于只能通过命令行接口 (CLI)。

更多详细信息，请参阅文章[标识适当 Azure SQL 数据库的 SKU 的本地数据库](dma-sku-recommend-sql-db.md)。

## <a name="dma-v36"></a>DMA v3.6

DMA v3.6 版本引入了"自动修复"受影响的最常见的迁移阻止程序的架构对象。

此发行版提供了以下迁移阻止程序的自动修复和行为更改的问题：

* 使用非限定 Join 语法的架构对象。
* 使用旧式 RAISEERROR 语句的架构对象。
* 使用整数文本的顺序的 SQL 语句。

DMA 执行自动架构转换为列出的问题受影响的对象，并提示用户进行确认，然后继续进行架构转换。 用户可以查看建议的代码更改，然后可以接受或拒绝任何给定的数据库对象的所有转换。

DMA 使用 Microsoft 程序合成 (PROSE) 技术来建议代码修复。 详细了解如何[PROSE](https://microsoft.github.io/prose/)。

## <a name="dma-v35"></a>DMA v3.5

DMA v3.5 版本还包括以下新增功能：

* 迁移到 Azure SQL 数据库 （基准检验测试表明过程将四次更快于使用早期版本的 DMA） 显著的性能改进。
* 内存占用量进一步优化以提高迁移工作流的稳定性。
* 架构和数据迁移期间跳过评估，（如果你已执行评估并解决任何重大架构对象，再迁移） 的功能。
* 若要使用时无效的网络共享路径提供对于备份文件，当执行升级的旧版本的 SQL Server 的本地到更高版本或 Azure Vm 上的 SQL Server 时遇到的故障的工具解决问题的修补程序。

## <a name="dma-v34"></a>DMA v3.4

DMA v3.4 版本还包括以下新增功能：

* 作为迁移到 Azure SQL 数据库的源 SQL Server 2017 的支持。
* 稳定性、 性能和评估规则正确性的增强功能。

## <a name="dma-v33"></a>DMA v3.3

DMA v3.3 版本，使迁移到新版本的 SQL Server 2017 中，在 Windows 和 Linux 上的本地 SQL Server 实例。 尽管 Windows 和 Linux 的总体迁移工作流是相同的适用于 Linux 迁移到 SQL Server 2017 需要几个其他注意事项。

### <a name="specifying-the-back-up-path"></a>指定的备份路径

Linux 和 Windows 使用不同的路径格式。 因此，迁移到 SQL Server 2017 Linux 上要求用户提供 Windows 和 Linux 版本的物理文件的位置的路径。 具体取决于物理文件的位置不同的方式，可以提供这两个版本的路径。
如果运行的计算机上为物理备份文件：

* Linux 中，使用 samba 共享，以与网络上的其他计算机共享文件。
* Windows，使用 mnt 命令来装载到运行 Linux 的计算机上共享。

> [!NOTE]
> 使用 samba 共享或 mnt 命令的详细信息已超出本文的讨论范围。

### <a name="migrating-windows-logins"></a>迁移 Windows 登录名

虽然在 Linux 上的 SQL Server 2017 正式支持的 Active Directory (AD) 的登录名迁移，但它需要额外的配置才能正常工作。 请参阅文章[使用 Linux 上的 SQL Server 的 Active Directory 身份验证](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication)有关 Active Directory 上设置登录名在 Linux 上的 SQL Server 2017 的详细信息。 在执行所需的配置，安装程序完成后可以将 Active Directory 登录名迁移像往常一样。 标准 SQL 身份验证的工作与不能有任何其他设置。

## <a name="dma-v32"></a>DMA v3.2

DMA 3.2 版版本还包括以下新增功能：

* 迁移架构和数据与新的迁移工作流启用从本地 SQL Server 数据库到 Azure SQL 数据库。
* 在架构迁移到 Azure SQL 数据库，DMA 脚本源数据库对象、 提供有关如何解决任何潜在的兼容性问题的指南，然后将您的架构部署到 Azure。

## <a name="dma-v31"></a>DMA v3.1

DMA v3.1 版本还包括以下新增功能：

* Azure SQL 数据库的数据库排序规则方面的改进的评估建议使用的不受支持的系统存储过程和 CLR 对象。
* 有关兼容性级别 130、 120、 110 和 100 时迁移到 Azure SQL 数据库的评估指南。

## <a name="dma-v30"></a>DMA v3.0

DMA 的 3.0 版版本扩展了 Azure SQL 数据库评估提供全面的建议，帮助解决与相关的问题：

* 迁移阻塞问题。
* 部分或不受支持的特性和功能。

## <a name="dma-v21"></a>DMA v2.1

DMA v2.1 版本还包括以下新增功能：

* 命令行支持在无人参与模式下，这有助于大规模运行评估运行评估。 更多详细信息，请参阅文章[运行数据迁移助手从命令行](dma-commandline.md)。
* 当用户启动和关闭 DMA 的性能改进。
* 配置 SQL 连接超时值的功能。更多详细信息，请参阅文章[配置设置的数据迁移助手](dma-configurationsettings.md)。

## <a name="dma-v20"></a>DMA v2.0

DMA 的 2.0 版包括改进了的延伸数据库功能建议，以提供最大限度地节省的存储空间的正确按优先顺序排列的表。

## <a name="dma-v10"></a>DMA v1.0

DMA 的 1.0 版版本是初始版本，它提供了：

* 发现的问题可能会影响升级到 SQL Server 的本地版本。 任何发现被描述为兼容性问题，并在分为以下几个方面：
  * 重大更改
  * 行为更改
  * 已弃用的功能
* 发现的数据库可受益于升级后的目标 SQL Server 平台中的新增功能。 任何发现结果被称为功能的建议，并在分为以下几个方面：
  * 性能
  * 安全性
  * 存储
* 若要执行评估的现代用户体验。

## <a name="see-also"></a>另请参阅

[数据迁移助手概述](../dma/dma-overview.md)
