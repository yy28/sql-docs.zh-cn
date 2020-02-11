---
title: 限制行（分区向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.typefilterexpression.f1
ms.assetid: eec8da8f-eab4-4ac4-a81d-995c814f88ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 59bff3eac690b7352b75d02bd7b266dfa8f303f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070205"
---
# <a name="restrict-rows-partition-wizard"></a>限制行（分区向导）
  可以使用 **“限制行”** 页，限制从指定表中检索、聚合并包括到分区中的行。  
  
> [!NOTE]  
>  只有在“指定源信息”**** 页中选择了单个表时，才会显示此页。  
  
> [!CAUTION]  
>  如果在“指定源信息”**** 页上的“可用表”**** 中指定了由另一个分区使用的表，则必须在“限制行”**** 页中提供查询，否则在多维数据集中会出现数据重复的风险。  
  
## <a name="options"></a>选项  
 **指定查询以限制行**  
 选择此选项可以输入查询，对进入“查询”**** 框中的行进行限制。  
  
 如果在选择此选项时 **“提供 WHERE 子句”** 为空，将使用一个从前面选择的表中检索所有列和所有行的 SQL 语句来填充该选项。  
  
 **查询**  
 键入或修改在处理分区过程中从表中检索行时所使用的 SQL 语句。  
  
> [!IMPORTANT]  
>  通过指定 WHERE 子句，可以将记录的子集用于此分区。 当多个分区都基于单一事实数据表时，防止数据重复很重要。  
  
 **查阅**  
 验证“查询”**** 中的语句是否为有效的 SQL 语句。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 多维数据 &#40;分区&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
