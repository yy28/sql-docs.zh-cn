---
title: ReadWriteMode 元素 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a109db366c2b165ccf466bdeab8b7d3bb9c4d69f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="readwritemode-element"></a>ReadWriteMode 元素
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  **ReadWriteMode**数据库属性指定数据库是否处于**ReadWrite**模式或**ReadOnly**模式。 只可能有两个属性值。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|ReadWrite|  
|基数|0-1：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[数据库](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 在中创建数据库**ReadWrite**仅限模式。 无法在创建数据库**ReadOnly**模式。  
  
 值**ReadWriteMode**元素被限制为下表中列出的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*ReadOnly*|不能向数据库应用任何更改或更新。|  
|*ReadWrite*|可以向数据库应用更改和更新。|  
  
## <a name="see-also"></a>另请参阅  
 [附加元素](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [附加和分离 Analysis Services 数据库](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [移动 Analysis Services 数据库](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [数据库 Readwritemode](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [切换 ReadOnly 和 ReadWrite 模式之间的 Analysis Services 数据库](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
