---
title: 启用了写功能的分区 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 13864dba5cac0274204050a8c78730de29f3321e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727171"
---
# <a name="write-enabled-partitions"></a>可写入的分区
  多维数据集中的数据通常为只读数据。 但在某些情况下，可能需要为分区启用写入。 使用可写入的分区，业务用户可以通过更改单元值并分析更改对多维数据集数据所产生的影响来研究方案。 向分区中写入时，客户端应用程序可以记录对分区中的数据所做的更改。 这些更改（称为写回数据）存储在单独的表中，并且不会覆盖度量值组中的任何现有数据。 但是，它们被作为多维数据集数据的一部分合并到了查询结果中。  
  
 可以对整个多维数据集或仅对多维数据集中的某些分区启用写操作。 启用写操作的维度各不相同但可以互补。 使用可写入的分区，用户可以更新分区单元，而启用写操作的维度则允许用户更新维度成员。 还可以组合使用这两个功能。 例如，启用写操作的多维数据集或可写入的分区可以不必包括任何启用写操作的维度。 **相关主题：**[启用写操作的维度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
> [!NOTE]  
>  如果要对数据源为 Microsoft Access 数据库的多维数据集启用写操作，则不要在多维数据集及其分区或维度的数据源定义中使用用于 ODBC 驱动程序的 Microsoft OLE DB 访问接口。 但可以使用 Microsoft Jet 4.0 OLE DB 访问接口或包括 Jet 4.0 OLE 的任何 Jet Service Pack 版本。 有关详细信息，请参阅 Microsoft 知识库文章[如何获取 Microsoft Jet 4.0 数据库引擎的最新 Service Pack](https://support.microsoft.com/?kbid=239114)。  
  
 只有其所有度量值均使用 `Sum` 聚合函数时，才能对该多维数据集启用写操作。 不能对链接度量值组和本地多维数据集启用写操作。  
  
## <a name="writeback-storage"></a>写回存储  
 业务用户所做的任何更改都以与当前显示值的差值形式存储在写回表中。 例如，如果最终用户将某个单元值从 90 更改为 100，则写回表中将存储 `+10` 以及更改发生的时间和执行更改的业务用户的相关信息。 累积更改的净效果显示给客户端应用程序。 将保留多维数据集中的原始值，并在写回表中记录更改的审核记录。  
  
 对叶单元更改和非叶单元更改的处理方式不同。 叶单元表示度量值和度量值组引用的每个维度中的叶成员的交集。 叶单元的值直接从事实数据表中获取，不能通过深化进一步细分。 如果对某个多维数据集或任意分区启用写操作，则可以对叶单元进行更改。 仅当客户端应用程序提供在组成非叶单元的叶单元当中分发更改的方法时，才能对非叶单元进行更改。 此进程（称为分配）通过多维表达式 (MDX) 中的 UPDATE CUBE 语句进行管理。 商业智能开发人员可以使用 UPDATE CUBE 语句包含分配功能。 有关详细信息，请参阅[UPDATE CUBE 语句 &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube)。  
  
> [!IMPORTANT]  
>  如果更新的单元不相互重叠，则 `Update Isolation Level` 连接字符串属性可用于提高 UPDATE CUBE 的性能。 有关详细信息，请参阅 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>。  
  
 无论客户端应用程序是否分发对非叶单元的更改，一旦对查询进行评估，写回表中的更改就会应用于叶单元和非叶单元，这样业务用户就可以查看更改对整个多维数据集的影响。  
  
 业务用户所做的更改将保留在单独的写回表中，可以按如下所示的方法来处理该表：  
  
-   转换为分区，以永久性地将更改合并到多维数据集中。 该操作可将度量值组设为只读。 您可以指定筛选表达式以选择要转换的更改。  
  
-   放弃，以将分区恢复到其原来状态。 该操作可使分区变为只读。  
  
## <a name="security"></a>安全性  
 仅当业务用户属于对多维数据集的单元拥有读/写访问权限的角色时，才允许该业务用户在多维数据集的写回表中记录更改。 对于每个角色，您都可以控制可更新和不可更新的多维数据集单元。 有关详细信息，请参阅[&#40;Analysis Services&#41;授予多维数据集或模型权限](../multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [启用写功能的维度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [聚合和聚合设计](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [Analysis Services 多维数据 &#40;分区&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [启用写功能的维度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
