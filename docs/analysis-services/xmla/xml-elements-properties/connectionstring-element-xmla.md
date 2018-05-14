---
title: ConnectionString 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: adb7382774e81e9b2c2f8d1aa26f5bad5f02774f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="connectionstring-element-xmla"></a>ConnectionString 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含连接字符串使用由容器的父[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)或[源](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|请参阅下表。|  
  
|祖先或父级|基数|  
|------------------------|-----------------|  
|[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|1-1：出现一次且仅出现一次的必需元素。|  
|[数据源](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)，[源](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关**位置**元素， **ConnectionString**元素包含所用的连接字符串**还原**或**同步**若要更新的本地数据源或连接到远程实例的命令。  
  
 有关**源**元素， **ConnectionString**元素包含所用的连接字符串**同步**命令以连接到源实例。  
  
 有关备份和还原对象的详细信息，请参阅[Backing Up，正在还原，和同步数据库 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>另请参阅  
 [还原元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [同步元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
