---
title: ConnectionString 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ConnectionString Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.connectionstring
- urn:schemas-microsoft-com:xml-analysis#ConnectionString
- http://schemas.microsoft.com/analysisservices/2003/engine#ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: 3b0575aa-79ed-4f14-ae7e-dd587af4cdb1
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7345d2a35d80a2ce4d72875c4afb082b57ec1a4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293207"
---
# <a name="connectionstring-element-xmla"></a>ConnectionString 元素 (XMLA)
  包含父级所使用的连接字符串[位置](location-element-xmla.md)或[源](source-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数的祖先或父级|基数|  
|[位置](location-element-xmla.md)|1-1：出现一次且仅出现一次的必需元素。|  
|[数据源](source-element-xmla.md)|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[位置](location-element-xmla.md)，[源](source-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对于 `Location` 元素，`ConnectionString` 元素包含 `Restore` 或 `Synchronize` 命令用于更新本地数据源或连接到远程实例的连接字符串。  
  
 对于 `Source` 元素，`ConnectionString` 元素包含 `Synchronize` 命令用于连接到源实例的连接字符串。  
  
 有关备份和还原对象的详细信息，请参阅[备份、 还原和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [Restore 元素&#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [Synchronize 元素&#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
