---
title: "PolyBase 指南 | Microsoft Docs"
ms.date: 12/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- "Hadoop import ×"
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
ms.assetid: b42b7d48-328a-4046-abe9-f73fd83212dc
caps.latest.revision: 26
author: barbkess
ms.author: barbkess
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 627fdce2e1c294343680b119e9b0c36fc3d8665d
ms.lasthandoff: 04/11/2017

---
# <a name="polybase-guide"></a>PolyBase 指南
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase 是一种技术，用于访问和合并所有来自 SQL Server 中的非关系和关系数据。  在 SQL Server 2016 中，它允许对 Hadoop 或 Azure blob 存储中的外部数据运行查询。 查询会进行优化以将计算推送到 Hadoop。 在 Azure SQL 数据仓库中，你可以从 Azure Blob 存储和 Azure Data Lake Store 导入数据。
  
可以使用 Transact-SQL (T-SQL) 语句在 SQL Server 中的关系表与存储在 Hadoop 或 Azure Blob 存储中的非关系数据之间来回导入和导出数据。 你还可以从 T-SQL 查询内查询外部数据并将其与关系数据联接。  
  
 若要使用 Polybase，请参阅 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 ![PolyBase 逻辑](../../relational-databases/polybase/media/polybase-logical.png "PolyBase 逻辑")  
  
## <a name="why-use-polybase"></a>为什么要用 PolyBase？  
若要作出正确决策，你需要同时分析关系数据和其他未构建到表中的数据 - 尤其是 Hadoop 数据。 除非有方法能够在不同数据存储类型之间传输数据，否则这将很难执行。 PolyBase 通过处理 SQL Server 外部的数据填补了这一差距。  
  
为了简单起见，PolyBase 不要求你向 Hadoop 或 Azure 环境安装其他的软件。 查询外部数据使用与查询数据库表一样的语法。 所有的一切均透明发生。 PolyBase 会在后台处理所有详细信息，且不需要任何 Hadoop 或 Azure 相关的知识便可成功使用 PolyBase。 
  
 PolyBase 能够：  
  
-   **查询存储在 Hadoop 中的数据。** 用户将数据存储在经济高效的分布式、可扩展系统中，例如 Hadoop。 PolyBase 使得使用 T-SQL 查询数据更加容易。  
  
-   **查询存储在 Azure blob 存储中的数据。** Azure blob 存储是一个方便存储供 Azure 服务使用的数据的位置。  PolyBase 使得使用 T-SQL 访问数据变得更加容易。  
  
-   **从 Hadoop、Azure blob 存储或 Azure Data Lake Store 导入数据** 通过从 Hadoop、Azure Blob 存储或 Azure Data Lake Store 将数据导入到关系表中，利用 Microsoft SQL 的列存储技术和分析功能的速度。 不需要单独的 ETL 或导入工具。  

  
-   **将数据导出到 Hadoop、Azure Blob 存储或 Azure Data Lake Store。** 将数据存档到 Hadoop、Azure Blob 存储或 Azure Data Lake Store，以获得经济高效的存储，并使数据保持联机以便于访问。  
  
-   **与 BI 工具集成** 结合使用 PolyBase 和 Microsoft 的商业智能和分析堆栈或使用任何与 SQL Server 兼容的第三方工具。  
  
## <a name="performance"></a>性能  
  
-   **将计算推送到 Hadoop。**查询优化器制定了基于开销的决策，以在执行此操作将提升查询性能时将计算推送到 Hadoop。  它使用外部表上的统计以制定基于开销的决策。   推送计算会创建 MapReduce 作业并利用 Hadoop 的分布计算资源。  
  
-   **缩放计算资源。** 若要提高查询性能，可以使用 SQL Server [PolyBase 扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)。 这使并行数据可以在 SQL Server 实例和 Hadoop 节点之间传输，并为处理外部数据添加计算资源。  
  
## <a name="polybase-guide-topics"></a>PolyBase 指南主题  
 本指南包括帮助你高效且有效地使用 PolyBase 的主题。  
  
|||  
|-|-|  
|**主题**|**说明**|  
|[PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)|安装和配置 PolyBase 的基本步骤。 这演示了如何创建指向 Hadoop 或 Azure blob 存储中数据的外部对象，并提供了查询示例。|  
|[PolyBase 受版本控制的功能摘要](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|描述 SQL Server、SQL 数据库和 SQL 数据仓库上支持哪些 PolyBase 功能。|  
|[PolyBase 扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)|通过使用 SQL Server 扩展组在 SQL Server 和 Hadoop 之间扩展并行度。|  
|[PolyBase 安装](../../relational-databases/polybase/polybase-installation.md)|使用安装向导或命令行工具安装 PolyBase 的参考和步骤。|  
|[PolyBase 配置](../../relational-databases/polybase/polybase-configuration.md)|为 PolyBase 配置 SQL Server 设置。  例如，配置计算下推和 kerberos 安全性。|  
|[PolyBase T-SQL 对象](../../relational-databases/polybase/polybase-t-sql-objects.md)|创建 PolyBase 用来定义和访问外部数据的 T-SQL 对象。|  
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|使用 T-SQL 语句来查询、导入或导出外部数据。|  
|[PolyBase 故障排除](../../relational-databases/polybase/polybase-troubleshooting.md)|管理 PolyBase Queries的技术。 使用动态管理视图 (DMV) 来监视 PolyBase Queries，并了解如何读取 PolyBase Queries 计划，以找出性能瓶颈。|  
  
  

