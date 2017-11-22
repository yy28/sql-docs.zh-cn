---
title: "在 DirectQuery 模型 （SSAS 表格） 中定义分区 |Microsoft 文档"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b680877b5ac907e143222b029d5d717145d3c2a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="define-partitions-in-directquery-models"></a>在 DirectQuery 模型中定义分区

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  本节介绍了如何在 DirectQuery 模型中使用分区。 有关表格模型中分区的更多常规信息，请参阅 [分区（SSAS 表格）](../../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
> [!NOTE]  
>  虽然表在 DirectQuery 模式下可以有多个分区，但只能指定其中一个分区在查询执行中使用。 一个分区要求可适用于所有兼容性级别的 DirectQuery 模型。  
  
## <a name="using-partitions-in-directquery-mode"></a>在 DirectQuery 模式下使用分区  
 对于每个表，您必须指定要用作 DirectQuery 数据源的单个分区。  如果存在多个分区，则在您切换模型以便启用 DirectQuery 模式时，默认情况下，在该表中已创建的第一个分区将标记为 DirectQuery 分区。 可以在以后通过使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的分区管理器来更改此设置。  
  
 为什么在 DirectQuery 模式下仅允许单个分区？  
  
 在表格模型中（与在 OLAP 模型中一样），表的分区是由 SQL 查询定义的。 创建分区定义的开发人员负责确保分区不重叠。 Analysis Services 不检查记录是属于一个分区还是多个分区。  
  
 缓存表格模型中分区的行为方式相同。 如果您在使用内存中模型，则在访问缓存时，将对每个分区计算 DAX 公式，并且合并结果。 但表格模型使用 DirectQuery 模式时，无法计算多个分区、合并结果以及将其转换到 SQL 语句中以便发送到关系数据存储区。 这样做可能会导致无法接受的性能损失，以及在聚合结果时潜在的不精确性。  
  
 因此，对于在 DirectQuery 模式下响应的查询，服务器使用已标记为 DirectQuery 访问的主分区的单个分区，称为 *DirectQuery 分区*。  此分区的定义中指定的 SQL 查询定义可用于在 DirectQuery 模式下响应查询的完整数据集。  
  
 如果未显式定义分区，则引擎只是向整个关系数据源发出 SQL 查询，执行 DAX 公式规定的任何基于集的操作，并且返回查询结果。  
  
  
## <a name="change-a-directquery-partition"></a>更改 DirectQuery 分区  
 因为在一个表中只能有一个分区可以指定为 DirectQuery 分区，所以，默认情况下，Analysis Services 使用在该表中创建的第一个分区。 在模型项目创作过程中，您可以通过使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的“分区管理器”对话框来更改 DirectQuery 分区。 对于部署的模型，您可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]来更改 DirectQuery 分区。  
  
#### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>更改表格模型项目的 DirectQuery 分区  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的模型设计器中，单击包含已分区表的表（选项卡）。  
  
2.  单击 **“表”** 菜单，然后单击 **“分区”**。  
  
3.  在“分区管理器”中，作为当前直接查询分区的分区由分区名称上的前缀 **(DirectQuery)** 指示。  
  
     从 **“分区”** 列表中选择一个不同的分区，然后单击 **“设置为 DirectQuery”**。 在选择当前 DirectQuery 分区时 **“设置为 DirectQuery”** 按钮未启用，并且在尚未为直接查询模式启用模型时不可见。  
  
4.  如果需要，请更改处理选项，然后单击 **“确定”**。  
  
#### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>更改已部署表格模型的 DirectQuery 分区  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的对象资源管理器中，打开模型数据库。  
  
2.  展开“表”节点，右键单击已分区表，然后选择“分区”。  
  
     为用于 DirectQuery 模式而指定的分区在分区名称上具有前缀 (DirectQuery)。  
  
3.  若要更改为其他分区，请单击 **“直接查询”** 工具栏图标以便打开 **“设置 DirectQuery 分区”** 对话框。 在尚未为直接查询启用的模型上，DirectQuery 工具栏图标不可用。  
  
4.  从 **“分区名称”** 下拉列表中选择一个不同的分区，然后根据需要更改该分区上的处理选项。  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>缓存模型和 DirectQuery 模型中的分区  
 配置 DirectQuery 分区时，必须指定分区的处理选项。  
  
 DirectQuery 分区有两个处理选项。 若要设置此属性，请使用 **中的** “分区管理器” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然后选择 **“处理选项”** 属性。 下表列出此属性的值，并说明在与连接字符串中的 DirectQueryUsage 属性结合使用时每个值的用途。  
  
|**连接字符串** 属性|**“处理选项”** 属性|说明|  
|------------------------------------|------------------------------------|-----------|  
|DirectQuery|绝不要处理此分区|模型使用仅限 DirectQuery 时，没必要进行处理。<br /><br /> 在混合模型中，您可以将 DirectQuery 分区配置为永远不会被处理。 例如，如果您正在对一个非常大的数据集进行操作，并且不想将完整结果添加到缓存中，则可以指定 DirectQuery 分区包含表中所有其他分区结果的并集，然后永远不处理该并集。 转到关系数据源的查询将不会受到影响，并且对缓存数据进行的查询将合并来自其他分区的数据|  
|DataView=Sample<br /><br /> 适用于使用示例数据视图的表格模型|允许处理分区|如果模型正在使用示例数据，则你可以处理要返回已筛选的数据集的表，该数据集将在模型设计过程中提供视觉提示。|  
|DirectQueryUsage=InMemory With DirectQuery<br /><br /> 适用于在内存中与 DirectQuery 组合模式下运行的表格 1100 或 1103 模型|允许处理分区|如果模型使用混合模式，则你应将相同的分区用于针对内存中和 DirectQuery 数据源的查询。|  
  
## <a name="see-also"></a>另请参阅  
 [分区（SSAS 表格）](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
