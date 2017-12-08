---
title: "写入的分区 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e161c0c7b9456101ae4f216a78560b1fec827686
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="partitions---write-enabled-partitions"></a>分区-写入的分区
  多维数据集中的数据通常为只读数据。 但在某些情况下，可能需要为分区启用写入。 使用可写入的分区，业务用户可以通过更改单元值并分析更改对多维数据集数据所产生的影响来研究方案。 向分区中写入时，客户端应用程序可以记录对分区中的数据所做的更改。 这些更改（称为写回数据）存储在单独的表中，并且不会覆盖度量值组中的任何现有数据。 但是，它们被作为多维数据集数据的一部分合并到了查询结果中。  
  
 可以对整个多维数据集或仅对多维数据集中的某些分区启用写操作。 启用写操作的维度各不相同但可以互补。 使用可写入的分区，用户可以更新分区单元，而启用写操作的维度则允许用户更新维度成员。 还可以组合使用这两个功能。 例如，启用写操作的多维数据集或可写入的分区可以不必包括任何启用写操作的维度。 **相关的主题：**[Write-Enabled 维度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
> [!NOTE]  
>  如果要对数据源为 Microsoft Access 数据库的多维数据集启用写操作，则不要在多维数据集及其分区或维度的数据源定义中使用用于 ODBC 驱动程序的 Microsoft OLE DB 访问接口。 但可以使用 Microsoft Jet 4.0 OLE DB 访问接口或包括 Jet 4.0 OLE 的任何 Jet Service Pack 版本。 有关详细信息，请参阅 Microsoft 知识库文章[如何获取 Microsoft Jet 4.0 数据库引擎的最新 service pack](http://support.microsoft.com/?kbid=239114)。  
  
 多维数据集可以写入-才会启用所有度量值使用**总和**聚合函数。 不能对链接度量值组和本地多维数据集启用写操作。  
  
## <a name="writeback-storage"></a>写回存储  
 业务用户所做的任何更改都以与当前显示值的差值形式存储在写回表中。 例如，如果最终用户为 100，值从 90 更改一个单元格值**+ 10**存储在写回表，以及更改与发出它的业务用户有关的信息的时间。 累积更改的净效果显示给客户端应用程序。 将保留多维数据集中的原始值，并在写回表中记录更改的审核记录。  
  
 对叶单元更改和非叶单元更改的处理方式不同。 叶单元表示度量值和度量值组引用的每个维度中的叶成员的交集。 叶单元的值直接从事实数据表中获取，不能通过深化进一步细分。 如果对某个多维数据集或任意分区启用写操作，则可以对叶单元进行更改。 仅当客户端应用程序提供在组成非叶单元的叶单元当中分发更改的方法时，才能对非叶单元进行更改。 此进程（称为分配）通过多维表达式 (MDX) 中的 UPDATE CUBE 语句进行管理。 商业智能开发人员可以使用 UPDATE CUBE 语句包含分配功能。 有关详细信息，请参阅[UPDATE CUBE 语句 &#40;MDX &#41;](../../mdx/mdx-data-manipulation-update-cube.md).  
  
> [!IMPORTANT]  
>  如果更新的单元不相互重叠，则 **Update Isolation Level** 连接字符串属性可用于提高 UPDATE CUBE 的性能。 有关详细信息，请参阅 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>。  
  
 无论客户端应用程序是否分发对非叶单元的更改，一旦对查询进行评估，写回表中的更改就会应用于叶单元和非叶单元，这样业务用户就可以查看更改对整个多维数据集的影响。  
  
 业务用户所做的更改将保留在单独的写回表中，可以按如下所示的方法来处理该表：  
  
-   转换为分区，以永久性地将更改合并到多维数据集中。 该操作可将度量值组设为只读。 您可以指定筛选表达式以选择要转换的更改。  
  
-   放弃，以将分区恢复到其原来状态。 该操作可使分区变为只读。  
  
## <a name="security"></a>安全性  
 仅当业务用户属于对多维数据集的单元拥有读/写访问权限的角色时，才允许该业务用户在多维数据集的写回表中记录更改。 对于每个角色，您都可以控制可更新和不可更新的多维数据集单元。 有关详细信息，请参阅[授予多维数据集或模型权限 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
## <a name="see-also"></a>另请参阅  
 [写入的维度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [聚合和聚合设计](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [分区（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [启用写操作的维度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
