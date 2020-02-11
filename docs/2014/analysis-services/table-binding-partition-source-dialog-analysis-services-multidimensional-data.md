---
title: 表绑定详细信息（"分区源" 对话框）（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitiontableselection.f1
ms.assetid: 67d05389-81ae-4a6b-947b-986d37ec72b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7f8ea36c8c3d49d4903379ed4450548fc760937a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067868"
---
# <a name="table-binding-detail-partition-source-dialog-box-analysis-services---multidimensional-data"></a>表绑定详细信息（“分区源”对话框）（Analysis Services - 多维数据）
  可以使用 **“分区源”** 对话框中的 **“表绑定”** 选项，指定为分区提供数据的事实数据表。 通过从 **“分区源”** 对话框中的 **“绑定类型”** 选项中选择 **“表绑定”** ，可以显示此窗格。  
  
## <a name="options"></a>选项  
 **度量值组**  
 显示此分区的度量值组。  
  
 **Look in**  
 选择包含此分区的源表的数据源或数据源视图。 默认情况下，将选择所选度量值组使用的数据源视图。  
  
 **筛选表**  
 键入字符串，用于按表名对“可用表”**** 中显示的表进行限制。  
  
 **查找表**  
 选择此项可以刷新“可用表”**** 中表的列表，如果在“筛选表”**** 中指定了字符串，则可以进一步限制该列表。  
  
 **可用表**  
 单击此项可选择要用作分区的源表的表。  
  
 如果 **“筛选表”** 中未指定任何筛选器，则对于 **“查找范围”** 中指定的数据源或数据源视图中的表，只要在结构上与 **“度量值组”** 中指定的度量值组所使用的事实数据表相似，就会在列表中列出。  
  
 如果 **“筛选表”** 中指定了筛选器，通过将筛选器与符合上述条件的表名进行对比，可以进一步限制列表。 只有那些包含 **“筛选表”** 中指定字符串的表才会显示。  
  
## <a name="see-also"></a>另请参阅  
 ["分区源" 对话框 &#40;Analysis Services 多维数据&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
