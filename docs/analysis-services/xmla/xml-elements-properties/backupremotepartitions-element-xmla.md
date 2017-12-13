---
title: "BackupRemotePartitions 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: BackupRemotePartitions Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.backupremotepartitions
- http://schemas.microsoft.com/analysisservices/2003/engine#BackupRemotePartitions
- urn:schemas-microsoft-com:xml-analysis#BackupRemotePartitions
helpviewer_keywords: BackupRemotePartitions element
ms.assetid: bd68bcf9-b324-4fa8-b6e5-1f5531f9992c
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 15c8e74fb81f36303391bb62924cf63aff3a9734
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="backupremotepartitions-element-xmla"></a>BackupRemotePartitions 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]确定是否父[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)命令备份与对象关联的远程分区。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Backup>  
   ...  
   <BackupRemotePartitions>...</BackupRemotePartitions>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 如果**BackupRemotePartitions**设置为**True**、**位置**包含一个或多个元素**位置**元素必须包含在**备份**命令，或出现错误。 有关备份和还原远程分区的详细信息，请参阅[Backing Up，正在还原，和同步数据库 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>另请参阅  
 [Locations 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)   
 [Location 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
