---
title: 指定源信息（分区向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifydsvandfacttables.f1
ms.assetid: b6c13587-c690-45d9-af90-b3d652afc55b
author: minewiskan
ms.author: owend
ms.openlocfilehash: a597d1f8f3b5720f2f7a688fdf2aabc7941a0ce1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940298"
---
# <a name="specify-source-information-partition-wizard"></a>指定源信息（分区向导）
  可以使用 **“指定源信息”** 页，选择要在其中创建分区的度量值组以及该分区的数据源视图和筛选表。  
  
> [!CAUTION]  
>   如果在其他分区所使用的 **“可用表”** 中指定了表，则必须在 **“限制行”** 页上提供查询，否则多维数据集中的数据可能会发生重复。  
  
## <a name="options"></a>选项  
 **度量值组**  
 选择此分区的度量值组。  
  
 **查找范围**  
 选择包含此分区的源表的数据源或数据源视图。 默认情况下，将选择该度量值组使用的数据源视图。  
  
 **筛选表**  
 键入字符串，用于按表名对“可用表”**** 中显示的表进行限制。  
  
 **查找表**  
 选择此项可以刷新“可用表”**** 中表的列表，如果在“筛选表”**** 中指定了字符串，则可以进一步限制该列表。  
  
 **可用表**  
 选择要用作分区的源表的表。 **分区向导** 将为 **“可用表”** 中所选的每一个表创建一个分区。  
  
 如果 **“筛选表”** 中未指定筛选条件，此选项将在数据源或数据源视图中列出 **“查找范围”** 中指定的所有表，以及与 **“度量值组”** 中指定的度量值组所使用的事实数据表结构相似的所有表。  
  
 如果在 **“筛选表”** 中指定了筛选条件，通过将该筛选条件与符合先前条件的表名进行对比，可以进一步限制列表。 只有那些包含 **“筛选表”** 中指定字符串的表才会显示。  
  
> [!NOTE]  
>  如果选择了多个表，则无法显示 **“限制行”** 页，也无法对从这些所选表创建的分区限制行。 若要对每个分区限制行，请为要从中创建分区的每一个表运行一次分区向导。  
  
## <a name="see-also"></a>另请参阅  
 [分区（Analysis Services - 多维数据）](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
