---
title: BackupRemotePartitions 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- BackupRemotePartitions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.backupremotepartitions
- http://schemas.microsoft.com/analysisservices/2003/engine#BackupRemotePartitions
- urn:schemas-microsoft-com:xml-analysis#BackupRemotePartitions
helpviewer_keywords:
- BackupRemotePartitions element
ms.assetid: bd68bcf9-b324-4fa8-b6e5-1f5531f9992c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e18d01ec48264d735a111bc002ca92b08c7b374
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108174"
---
# <a name="backupremotepartitions-element-xmla"></a>BackupRemotePartitions 元素 (XMLA)
  确定是否父级[备份](../xml-elements-commands/backup-element-xmla.md)命令备份与对象关联的远程分区。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Backup>  
   ...  
   <BackupRemotePartitions>...</BackupRemotePartitions>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../xml-elements-commands/backup-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 如果将 `BackupRemotePartitions` 设置为 `True`，则包含一个或多个 `Locations` 元素的 `Location` 元素必须包括在 `Backup` 命令中，否则将出现错误。 有关备份和还原远程分区的详细信息，请参阅[备份、 还原和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [Locations 元素&#40;XMLA&#41;](locations-element-xmla.md)   
 [Location 元素&#40;XMLA&#41;](location-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
