---
title: ReadWriteMode 元素 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0d528567e22c3ba19b49eefff10d886703a0d29a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994849"
---
# <a name="readwritemode-element"></a>ReadWriteMode 元素
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  **ReadWriteMode**数据库属性指定数据库是否处于**ReadWrite**模式中或在**ReadOnly**模式。 只可能有两个属性值。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素的特性  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|ReadWrite|  
|基数|0-1：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[“数据库”](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 数据库中创建**ReadWrite**仅限模式。 不能在中创建数据库**ReadOnly**模式。  
  
 值**ReadWriteMode**元素仅限于下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*只读*|不能向数据库应用任何更改或更新。|  
|*ReadWrite*|可以向数据库应用更改和更新。|  
  
## <a name="see-also"></a>另请参阅
 [附加元素](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [附加和分离 Analysis Services 数据库](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [移动 Analysis Services 数据库](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [数据库 Readwritemode](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [切换 ReadOnly 和 ReadWrite 模式之间的 Analysis Services 数据库](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
