---
title: ConnectionString 元素 (XMLA) |Microsoft 文档
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
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 12d69bfe2b8dc8bda91bc873167bb3208203d728
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015776"
---
# <a name="connectionstring-element-xmla"></a>ConnectionString 元素 (XMLA)
  包含连接字符串使用由容器的父[位置](location-element-xmla.md)或[源](source-element-xmla.md)元素。  
  
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
  
 有关备份和还原对象的详细信息，请参阅[Backing Up、 正在还原，和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [Restore 元素&#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [同步元素&#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  