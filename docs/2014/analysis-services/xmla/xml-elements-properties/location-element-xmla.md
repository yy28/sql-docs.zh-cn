---
title: Location 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Location Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords:
- Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0277ab50eb7390d3272c309df8dc865ff088c89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48107607"
---
# <a name="location-element-xmla"></a>Location 元素 (XMLA)
  包含信息的远程服务器的父[备份](../xml-elements-commands/backup-element-xmla.md)，[还原](../xml-elements-commands/restore-element-xmla.md)，或[同步](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Location>  
```  
  
```  
  
<File>...</File> <!-- for Backup and Restore only -->  
<DataSourceID>...</DataSourceID>  
<DataSourceType>...</DataSourceType> <!-- for Restore and Synchronize only -->  
<ConnectionString>...</ConnectionString> <!-- for Restore and Synchronize only -->  
<Folders>...</Folders> <!-- for Restore and Synchronize only -->  
```  
  
```  
  
   </Location>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../xml-elements-commands/backup-element-xmla.md)，[还原](../xml-elements-commands/restore-element-xmla.md)，[同步](../xml-elements-commands/synchronize-element-xmla.md)|  
  
## <a name="child-elements"></a>子元素  
  
|祖先或父级|子元素|  
|------------------------|-------------------|  
|[备份](id-element-xmla.md)，[文件](file-element-xmla.md)|  
|[还原](connectionstring-element-xmla.md)， [DataSourceID](datasourceid-element-xmla.md)， [DataSourceType](type-element-xmla.md)，[文件](file-element-xmla.md)，[文件夹](folders-element-xmla.md)|  
|[同步](../xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](connectionstring-element-xmla.md)， [DataSourceID](datasourceid-element-xmla.md)， [DataSourceType](type-element-xmla.md)，[文件夹](folders-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 有关`Backup`命令，`Location`元素提供有关创建的远程实例的远程备份文件的信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 对于 `Restore` 命令，`Location` 元素提供有关标识和连接到远程 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的信息，以及用于还原该远程实例上的远程分区的远程备份文件的信息。  
  
 对于 `Synchronize` 命令，`Location` 元素根据父 `DataSourceType` 命令的 `Synchronize` 元素的值，描述描述目标实例或必须与目标实例同步的源实例上定义的远程实例要使用的数据源。  
  
 有关备份和还原远程实例的详细信息，请参阅[备份和还原对象 (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [BackupRemotePartitions 元素&#40;XMLA&#41;](backupremotepartitions-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
