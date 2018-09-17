---
title: PolyBase 指南 | Microsoft Docs
ms.date: 05/31/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: quickstart
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c31f9538f3429ff4ae1182ee0cd974996cc705a6
ms.sourcegitcommit: 82bb56269faf3fb5dd1420418e32a0a6476780cc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2018
ms.locfileid: "43694720"
---
# <a name="polybase-guide"></a>PolyBase 指南

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

借助 PolyBase，SQL Server 2016 实例可处理从 Hadoop 中读取数据的 Transact-SQL 查询。 同一查询还可以访问 SQL Server 中的关系表。 借助 PolyBase，同一查询还可以联接 Hadoop 和 SQL Server 中的数据。 在 SQL Server 中，[外部表](../../t-sql/statements/create-external-table-transact-sql.md)或[外部数据源](../../t-sql/statements/create-external-data-source-transact-sql.md)提供对 Hadoop 的连接。

PolyBase 对以下 Microsoft SQL 产品提供这些相同功能：

- SQL Server 2016 及更高版本
- 分析平台系统（旧称为“并行数据仓库”）
- Azure SQL 数据仓库

PolyBase 将一些计算推送到 Hadoop 节点，以优化总体查询。 不过，PolyBase 外部访问不仅限于 Hadoop。 其他未结构化的非关系表也受支持，如带分隔符的文本文件。

#### <a name="data-import-and-export"></a>数据导入和导出

借助 PolyBase 的基础帮助，T-SQL 查询还可以将数据导入和导出 Azure Blob 存储。 此外，借助 PolyBase，Azure SQL 数据仓库还可以将数据导入和导出 Azure Data Lake Store 和 Azure Blob 存储。

若要使用 Polybase，请参阅 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)。
  
![PolyBase 逻辑](../../relational-databases/polybase/media/polybase-logical.png "PolyBase 逻辑")

## <a name="why-use-polybase"></a>为什么要用 PolyBase？

过去联接 SQL Server 数据与外部数据的难度更大。 具体有下列两种不方便的方法：

- 传输一半数据，这样所有数据都采用一种格式或其他格式。
- 查询两个数据源，然后编写自定义查询逻辑，以在客户端一级联接和集成数据。

PolyBase 使用 T-SQL 来联接数据，因此可避免使用这两种不方便的方法

为了简单起见，PolyBase 不要求在 Hadoop 环境中安装其他软件。 查询外部数据所用的 T-SQL 语法也是用于查询数据库表的语法。 PolyBase 实现的所有支持操作全都以透明方式发生。 查询作者无需对 Hadoop 有任何了解。

PolyBase 能够：

- **通过 SQL Server 或 PDW 查询 Hadoop 中存储的数据。** 用户将数据存储在经济高效的分布式、可扩展系统中，例如 Hadoop。 PolyBase 使得使用 T-SQL 查询数据更加容易。

- **查询存储在 Azure Blob 存储中的数据。** Azure blob 存储是一个方便存储供 Azure 服务使用的数据的位置。  PolyBase 使得使用 T-SQL 访问数据变得更加容易。

- **导入 Hadoop、Azure Blob 存储或 Azure Data Lake Store 中的数据。** 通过将 Hadoop、Azure Blob 存储或 Azure Data Lake Store 中的数据导入到关系表中，利用 Microsoft SQL 的列存储技术和分析功能的速度优势。 不需要单独的 ETL 或导入工具。

- **将数据导出到 Hadoop、Azure Blob 存储或 Azure Data Lake Store。** 将数据存档到 Hadoop、Azure Blob 存储或 Azure Data Lake Store，以获得经济高效的存储，并使数据保持联机以便于访问。

- **与 BI 工具集成** 结合使用 PolyBase 和 Microsoft 的商业智能和分析堆栈，或使用任何与 SQL Server 兼容的第三方工具。

## <a name="performance"></a>“性能”

- **将计算推送到 Hadoop。** 查询优化器制定了基于成本的决策，以在执行此操作将提升查询性能时将计算推送到 Hadoop。  它使用外部表上的统计以制定基于开销的决策。 推送计算会创建 MapReduce 作业并利用 Hadoop 的分布计算资源。

- **缩放计算资源。** 若要提高查询性能，可以使用 SQL Server [PolyBase 横向扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)。 这使并行数据可以在 SQL Server 实例和 Hadoop 节点之间传输，并为处理外部数据添加计算资源。

## <a name="polybase-guide-topics"></a>PolyBase 指南主题

本指南包括帮助你高效且有效地使用 PolyBase 的主题。

|||
|-|-|
|**主题**|**Description**|
|[PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)|安装和配置 PolyBase 的基本步骤。 这演示了如何创建指向 Hadoop 或 Azure blob 存储中数据的外部对象，并提供了查询示例。|
|[PolyBase 受版本控制的功能摘要](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|描述 SQL Server、SQL 数据库和 SQL 数据仓库上支持哪些 PolyBase 功能。|
|[PolyBase 横向扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)|通过使用 SQL Server 横向扩展组在 SQL Server 和 Hadoop 之间横向扩展并行度。|
|[PolyBase 安装](../../relational-databases/polybase/polybase-installation.md)|使用安装向导或命令行工具安装 PolyBase 的参考和步骤。|
|[PolyBase 配置](../../relational-databases/polybase/polybase-configuration.md)|为 PolyBase 配置 SQL Server 设置。  例如，配置计算下推和 kerberos 安全性。|
|[PolyBase T-SQL 对象](../../relational-databases/polybase/polybase-t-sql-objects.md)|创建 PolyBase 用来定义和访问外部数据的 T-SQL 对象。|
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|使用 T-SQL 语句来查询、导入或导出外部数据。|
|[PolyBase 故障排除](../../relational-databases/polybase/polybase-troubleshooting.md)|管理 PolyBase Queries的技术。 使用动态管理视图 (DMV) 来监视 PolyBase Queries，并了解如何读取 PolyBase Queries 计划，以找出性能瓶颈。|
| &nbsp; | &nbsp; |
  
