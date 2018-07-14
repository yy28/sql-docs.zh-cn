---
title: DataSourceID 元素 (XMLA) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e96d9386319fa9d850a755519fad7360da8ec3b0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231817"
---
# <a name="datasourceid-element-xmla"></a>DataSourceID 元素 (XMLA)
  标识使用的数据源[位置](location-element-xmla.md)期间[备份](../xml-elements-commands/backup-element-xmla.md)，[还原](../xml-elements-commands/restore-element-xmla.md)，或者[同步](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
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
  
 有关备份和还原远程分区的详细信息，请参阅[备份、 还原和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [ConnectionString 元素&#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [DataSourceType 元素&#40;XMLA&#41;](type-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
