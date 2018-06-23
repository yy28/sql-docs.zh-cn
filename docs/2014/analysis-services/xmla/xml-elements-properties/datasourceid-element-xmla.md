---
title: DataSourceID 元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DataSourceID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.datasourceid
- urn:schemas-microsoft-com:xml-analysis#DataSourceID
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceID
helpviewer_keywords:
- DataSourceID element
ms.assetid: 695522c7-acca-420a-a5fb-f01f3fd9a96b
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 2adec20f28e51639352dc89c70b6682e4df240fc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123700"
---
# <a name="datasourceid-element-xmla"></a>DataSourceID 元素 (XMLA)
  标识使用的数据源[位置](location-element-xmla.md)期间元素[备份](../xml-elements-commands/backup-element-xmla.md)，[还原](../xml-elements-commands/restore-element-xmla.md)，或[同步](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Location>  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[位置](location-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DataSourceID` 元素包含标识远程实例的源实例上的数据源名称，将在该远程实例上备份、还原或同步远程分区信息。  
  
 有关备份和还原远程分区的详细信息，请参阅[Backing Up、 正在还原，和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [ConnectionString 元素&#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [DataSourceType 元素&#40;XMLA&#41;](type-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  