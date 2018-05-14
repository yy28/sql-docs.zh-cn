---
title: DataSourceType 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21b95e057951058cc8b28e9be5020703da95b8db
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="datasourcetype-element-xmla"></a>DataSourceType 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指示是否[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)为指定的元素[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)或[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令是本地还是远程。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*远程*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **DataSourceType**元素确定数据源是否由定义**位置**元素包含的本地数据源或远程数据源。 有关备份和还原远程分区的详细信息，请参阅[Backing Up，正在还原，和同步数据库 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*本地*|**位置**元素定义的本地数据源。 如果使用此值，则**还原**和**同步**命令使用中定义的信息**位置**元素更新数据源检索从中指定备份文件**文件**元素**备份**命令或中指定的数据库**源**元素**同步**命令，在中标识**DataSourceID**元素**位置**元素。<br /><br /> 如果使用此值，则使用关系 OLAP (ROLAP) 存储的对象在还原或同步之后可以对自己的数据和元数据使用不同的数据库。<br /><br /> 注意： ROLAP 数据，如维度表或写回表中的数据不还原或同步。 只还原或同步 ROLAP 对象的元数据。|  
|*远程*|**位置**元素定义一个远程数据源。 如果使用此值，则**还原**和**同步**命令使用中定义的信息**位置**元素来还原或同步远程分区从备份文件中指定**文件**元素**备份**命令或中指定的数据库**源**元素**同步**命令，在中标识的远程实例**DataSourceID**的**位置**元素。|  
  
## <a name="see-also"></a>另请参阅  
 [ConnectionString 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)   
 [DataSourceID 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
