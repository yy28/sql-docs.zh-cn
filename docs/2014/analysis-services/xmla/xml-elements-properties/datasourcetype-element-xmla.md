---
title: DataSourceType 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataSourceType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DataSourceType
- microsoft.xml.analysis.datasourcetype
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceType
helpviewer_keywords:
- DataSourceType element
ms.assetid: f5a348b1-911b-4139-832e-4bcb6d80a728
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 54e374aad3980582f0653bc2e36c519b87d4a27b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169127"
---
# <a name="datasourcetype-element-xmla"></a>DataSourceType 元素 (XMLA)
  指示是否[位置](location-element-xmla.md)为指定的元素[还原](../xml-elements-commands/restore-element-xmla.md)或[同步](../xml-elements-commands/synchronize-element-xmla.md)命令是本地还是远程。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*远程*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[位置](location-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `DataSourceType` 元素确定 `Location` 元素定义的数据源包含的是本地数据源还是远程数据源。 有关备份和还原远程分区的详细信息，请参阅[备份、 还原和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*本地*|`Location` 元素定义本地数据源。 如果使用此值，则 `Restore` 和 `Synchronize` 命令使用在 `Location` 元素中定义的信息更新数据源，该数据源是从 `File` 命令的 `Backup` 元素中指定的备份文件中或 `Source` 命令的 `Synchronize` 元素中指定的数据库中检索的，在 `DataSourceID` 元素的 `Location` 元素中标识。<br /><br /> 如果使用此值，则使用关系 OLAP (ROLAP) 存储的对象在还原或同步之后可以对自己的数据和元数据使用不同的数据库。 **注意：** 不还原或同步 ROLAP 数据，如维度表或写回表中的数据。 只还原或同步 ROLAP 对象的元数据。|  
|*远程*|`Location` 元素定义远程数据源。 如果使用此值，则 `Restore` 和 `Synchronize` 命令使用在 `Location` 元素中定义的信息将远程分区（从 `File` 命令的 `Backup` 元素中指定的备份文件中或在 `Source` 命令的 `Synchronize` 元素中指定的数据库中检索的）还原或同步到 `DataSourceID` 元素的 `Location` 中标识的远程实例上。|  
  
## <a name="see-also"></a>请参阅  
 [ConnectionString 元素&#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [DataSourceID 元素&#40;XMLA&#41;](id-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
