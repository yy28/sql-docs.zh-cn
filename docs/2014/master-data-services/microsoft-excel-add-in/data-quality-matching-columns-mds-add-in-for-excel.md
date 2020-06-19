---
title: 数据质量匹配列 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 939ec9727cc81ce3b206b8bc7ca3ed8dd62c3877
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961297"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>数据质量匹配列（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中，匹配数据后，在功能区上的“数据质量”组中，可单击“显示详细信息”以显示提供匹配详细信息的列********。  
  
 下表显示匹配数据时显示的列。  
  
|名称|说明|  
|----------|-----------------|  
|**CLUSTER_ID**|用于对相似记录进行分组的唯一标识符。 所有相似的行都具有相同的 **CLUSTER_ID**。 如果没有为某一行显示 **CLUSTER_ID** ，则找不到相似的记录。|  
|**RECORD_ID**|用于标识记录的唯一标识符。 与在 MDS 存储库中存储的代码值相似，它是用于标识记录的值。 每次出现匹配时都将自动生成该值。|  
|**PIVOT_MARK**|其他记录与其进行比较的任意记录；它不具有得分值。|  
|**分值**|表示组中的记录与透视记录的相似程度。 该得分是由 DQS 确定的。 如果没有显示任何得分，则该记录是其他记录的透视记录，或者找不到匹配项。|  
  
## <a name="see-also"></a>另请参阅  
 [MDS Add-in for Excel 中的数据质量匹配](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [匹配相似的数据 &#40;MDS Add-in for Excel&#41;](match-similar-data-mds-add-in-for-excel.md)   
 [数据匹配](../../data-quality-services/data-matching.md)  
  
  
