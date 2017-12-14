---
title: "PolyBase 指南 | Microsoft Docs"
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine-polybase
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
caps.latest.revision: "26"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f7ce518d2588e07ae90842f92a7e9ee47cfc5543
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="polybase-guide"></a>PolyBase 指南
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]PolyBase 是一种可通过 t-sql 语言访问数据库外部数据的技术。  在 SQL Server 2016 中，可以对 Hadoop 中的外部数据运行查询或将数据导入/导出 Azure Blob 存储。 查询会进行优化以将计算推送到 Hadoop。 在 Azure SQL 数据仓库中，可以将数据导入/导出 Azure Blob 存储和 Azure Data Lake Store。
  
  
 若要使用 Polybase，请参阅 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 ![PolyBase 逻辑](../../relational-databases/polybase/media/polybase-logical.png "PolyBase 逻辑")  
  
## <a name="why-use-polybase"></a>为什么要用 PolyBase？  
若要作出正确决策，你需要同时分析关系数据和其他未构建到表中的数据 - 尤其是 Hadoop 数据。 除非有方法能够在不同数据存储类型之间传输数据，否则这将很难执行。 PolyBase 通过处理 SQL Server 外部的数据填补了这一差距。  
  
为了简单起见，PolyBase 不要求向 Hadoop 环境安装其他软件。 查询外部数据使用与查询数据库表一样的语法。 所有的一切均透明发生。 PolyBase 会在后台处理所有详细信息，并且最终用户不需要 Hadoop 的任何相关知识便可查询外部表。 
  
 PolyBase 能够：  
  
-   **通过 SQL Server 或 PDW 查询 Hadoop 中存储的数据。** 用户将数据存储在经济高效的分布式、可扩展系统中，例如 Hadoop。 PolyBase 使得使用 T-SQL 查询数据更加容易。  
  
-   **查询存储在 Azure Blob 存储中的数据。** Azure blob 存储是一个方便存储供 Azure 服务使用的数据的位置。  PolyBase 使得使用 T-SQL 访问数据变得更加容易。  
  
-   **从 Hadoop、Azure Blob 存储或 Azure Data Lake Store 导入数据** 通过将数据从 Hadoop、Azure Blob 存储或 Azure Data Lake Store 导入到关系表中，利用 Microsoft SQL 的列存储技术和分析功能的速度。 不需要单独的 ETL 或导入工具。  

-   **将数据导出到 Hadoop、Azure Blob 存储或 Azure Data Lake Store。** 将数据存档到 Hadoop、Azure Blob 存储或 Azure Data Lake Store，以获得经济高效的存储，并使数据保持联机以便于访问。  
  
-   **与 BI 工具集成** 结合使用 PolyBase 和 Microsoft 的商业智能和分析堆栈或使用任何与 SQL Server 兼容的第三方工具。  
  
## <a name="performance"></a>性能  
  
-   **将计算推送到 Hadoop。**查询优化器制定了基于开销的决策，以在执行此操作将提升查询性能时将计算推送到 Hadoop。  它使用外部表上的统计以制定基于开销的决策。   推送计算会创建 MapReduce 作业并利用 Hadoop 的分布计算资源。  
  
-   **缩放计算资源。** 若要提高查询性能，可以使用 SQL Server [PolyBase 横向扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)。 这使并行数据可以在 SQL Server 实例和 Hadoop 节点之间传输，并为处理外部数据添加计算资源。  
  
## <a name="polybase-guide-topics"></a>PolyBase 指南主题  
 本指南包括帮助你高效且有效地使用 PolyBase 的主题。  
  
|||  
|-|-|  
|**主题**|**说明**|  
|[PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)|安装和配置 PolyBase 的基本步骤。 这演示了如何创建指向 Hadoop 或 Azure blob 存储中数据的外部对象，并提供了查询示例。|  
|[PolyBase 受版本控制的功能摘要](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|描述 SQL Server、SQL 数据库和 SQL 数据仓库上支持哪些 PolyBase 功能。|  
|[PolyBase 横向扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)|通过使用 SQL Server 横向扩展组在 SQL Server 和 Hadoop 之间横向扩展并行度。|  
|[PolyBase 安装](../../relational-databases/polybase/polybase-installation.md)|使用安装向导或命令行工具安装 PolyBase 的参考和步骤。|  
|[PolyBase 配置](../../relational-databases/polybase/polybase-configuration.md)|为 PolyBase 配置 SQL Server 设置。  例如，配置计算下推和 kerberos 安全性。|  
|[PolyBase T-SQL 对象](../../relational-databases/polybase/polybase-t-sql-objects.md)|创建 PolyBase 用来定义和访问外部数据的 T-SQL 对象。|  
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|使用 T-SQL 语句来查询、导入或导出外部数据。|  
|[PolyBase 故障排除](../../relational-databases/polybase/polybase-troubleshooting.md)|管理 PolyBase Queries的技术。 使用动态管理视图 (DMV) 来监视 PolyBase Queries，并了解如何读取 PolyBase Queries 计划，以找出性能瓶颈。|  
  
  
