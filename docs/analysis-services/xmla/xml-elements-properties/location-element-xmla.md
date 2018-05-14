---
title: Location 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ea049b70ee2aa41a1e2fc1e7204be658f4f0bd6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="location-element-xmla"></a>Location 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父级的信息的远程服务器[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)，或[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)，[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|请参阅下表。|  
  
|祖先或父级|子元素|  
|------------------------|-------------------|  
|[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|[DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)，[文件](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)|  
|[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)， [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)， [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md)，[文件](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)，[文件夹](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)， [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)， [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md)，[文件夹](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 有关**备份**命令，**位置**元素提供有关创建的远程实例的远程备份文件信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 有关**还原**命令，**位置**元素提供有关标识和连接到远程信息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，以及用于还原远程的远程备份文件在该远程实例上的分区。  
  
 有关**同步**命令，**位置**元素描述要使用的目标实例的数据源，或者必须与同步源实例上定义的远程实例目标实例，具体取决于值**DataSourceType**的父元素**同步**命令。  
  
 有关备份和还原远程实例的详细信息，请参阅[备份和还原对象 (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另请参阅  
 [BackupRemotePartitions 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
