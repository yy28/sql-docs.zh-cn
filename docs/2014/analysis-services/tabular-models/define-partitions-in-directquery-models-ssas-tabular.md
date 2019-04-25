---
title: 分区和 DirectQuery 模式 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f445b32e0c580cde10f38a22b3d26270d927c5a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757324"
---
# <a name="partitions-and-directquery-mode-ssas-tabular"></a>分区和 DirectQuery 模式（SSAS 表格）
  本节介绍了如何在 DirectQuery 模型中使用分区。 有关表格模型中分区的更多常规信息，请参阅 [分区（SSAS 表格）](partitions-ssas-tabular.md)。  
  
 有关如何更改的分区的使用或查看有关分区的信息的说明，请参阅[更改 DirectQuery 分区&#40;SSAS 表格&#41;](../change-the-directquery-partition-ssas-tabular.md)。  
  
## <a name="using-partitions-in-directquery-mode"></a>在 DirectQuery 模式下使用分区  
 对于每个表，您必须指定要用作 DirectQuery 数据源的单个分区。  如果存在多个分区，则在您切换模型以便启用 DirectQuery 模式时，默认情况下，在该表中已创建的第一个分区将标记为 DirectQuery 分区。 可以在以后通过使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的分区管理器来更改此设置。  
  
 为什么在 DirectQuery 模式下仅允许单个分区？  
  
 在表格模型中（与在 OLAP 模型中一样），表的分区是由 SQL 查询定义的。 创建分区定义的开发人员负责确保分区不重叠。 Analysis Services 不检查记录是属于一个分区还是多个分区。  
  
 缓存表格模型中分区的行为方式相同。 如果您在使用内存中模型，则在访问缓存时，将对每个分区计算 DAX 公式，并且合并结果。 但表格模型使用 DirectQuery 模式时，无法计算多个分区、合并结果以及将其转换到 SQL 语句中以便发送到关系数据存储区。 这样做可能会导致无法接受的性能损失，以及在聚合结果时潜在的不精确性。  
  
 因此，对于在 DirectQuery 模式下响应的查询，服务器使用已标记为 DirectQuery 访问的主分区的单个分区，称为 *DirectQuery 分区*。  此分区的定义中指定的 SQL 查询定义可用于在 DirectQuery 模式下响应查询的完整数据集。  
  
 如果未显式定义分区，则引擎只是向整个关系数据源发出 SQL 查询，执行 DAX 公式规定的任何基于集的操作，并且返回查询结果。  
  
 如果您在某个表中有多个分区，并且将一个分区选择作为 DirectQuery 分区，则默认情况下所有其他分区将标记为仅供内存中使用。  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>缓存模型和 DirectQuery 模型中的分区  
 配置 DirectQuery 分区时，必须指定分区的处理选项。  
  
 DirectQuery 分区有两个处理选项。 若要设置此属性，请使用 **中的** “分区管理器” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然后选择 **“处理选项”** 属性。 下表列出此属性的值，并说明在与连接字符串中的 DirectQueryUsage 属性结合使用时每个值的用途。  
  
|**DirectQueryUsage**属性|**“处理选项”** 属性|说明|  
|-----------------------------------|------------------------------------|-----------|  
|DirectQuery|绝不要处理此分区|模型使用仅限 DirectQuery 时，没必要进行处理。<br /><br /> 在混合模型中，您可以将 DirectQuery 分区配置为永远不会被处理。 例如，如果您正在对一个非常大的数据集进行操作，并且不想将完整结果添加到缓存中，则可以指定 DirectQuery 分区包含表中所有其他分区结果的并集，然后永远不处理该并集。 转到关系数据源的查询将不会受到影响，并且对缓存数据进行的查询将合并来自其他分区的数据|  
|InMemory 以及 DirectQuery|允许处理分区|如果模型使用混合模式，则您应将相同的分区用于针对内存中的查询和针对 DirectQuery 数据源的查询。|  
  
## <a name="see-also"></a>请参阅  
 [分区（SSAS 表格）](partitions-ssas-tabular.md)  
  
  
