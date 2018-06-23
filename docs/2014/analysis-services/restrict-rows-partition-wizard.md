---
title: 限制行 （分区向导） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.partitionwizard.typefilterexpression.f1
ms.assetid: eec8da8f-eab4-4ac4-a81d-995c814f88ca
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5305400b58951e6a8090651fa50bfcad985cecaa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015992"
---
# <a name="restrict-rows-partition-wizard"></a>限制行（分区向导）
  可以使用 **“限制行”** 页，限制从指定表中检索、聚合并包括到分区中的行。  
  
> [!NOTE]  
>  只有在“指定源信息”页中选择了单个表时，才会显示此页。  
  
> [!CAUTION]  
>  如果在“指定源信息”页上的“可用表”中指定了由另一个分区使用的表，则必须在“限制行”页中提供查询，否则在多维数据集中会出现数据重复的风险。  
  
## <a name="options"></a>“常规”  
 **指定查询以限制行**  
 选择此选项可以输入查询，对进入“查询”框中的行进行限制。  
  
 如果在选择此选项时 **“提供 WHERE 子句”** 为空，将使用一个从前面选择的表中检索所有列和所有行的 SQL 语句来填充该选项。  
  
 **“数据集属性”**  
 键入或修改在处理分区过程中从表中检索行时所使用的 SQL 语句。  
  
> [!IMPORTANT]  
>  通过指定 WHERE 子句，可以将记录的子集用于此分区。 当多个分区都基于单一事实数据表时，防止数据重复很重要。  
  
 **检查**  
 验证“查询”中的语句是否为有效的 SQL 语句。  
  
## <a name="see-also"></a>请参阅  
 [分区&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  