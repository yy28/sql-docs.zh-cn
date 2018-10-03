---
title: 备份元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Backup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Backup
- http://schemas.microsoft.com/analysisservices/2003/engine#Backup
- microsoft.xml.analysis.backup
helpviewer_keywords:
- Backup command
ms.assetid: 5bcbc14c-9db9-45b2-99de-f3a265bcb0c4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 59efda960de14ae96b0c7c948b66c89980d8f990
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216491"
---
# <a name="backup-element-xmla"></a>Backup 元素 (XMLA)
  备份[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库添加到备份文件。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Backup>  
      <Object>...</Object>  
      <File>...</File>  
      <Security>...</Security>  
      <ApplyCompression>...</ApplyCompression>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <BackupRemotePartitions>...</BackupRemotePartitions>  
      <Locations>...</Locations>  
   </Backup>  
</Command>  
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
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md)， [ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md)， [BackupRemotePartitions](../xml-elements-properties/backupremotepartitions-element-xmla.md)，[文件](../xml-elements-properties/file-element-xmla.md)，[位置](../xml-elements-properties/locations-element-xmla.md)， [对象](../xml-elements-properties/object-element-xmla.md)，[密码](../xml-elements-properties/password-element-xmla.md)，[安全](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `Backup`命令备份[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定的数据库[对象](../xml-elements-properties/object-element-xmla.md)到备份文件，还可以选择将远程分区备份到远程备份文件的元素。 如果 `Object` 元素指向非 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库对象，则会出错。  
  
 哪些信息`Backup`命令将备份取决于数据库中的对象使用的存储模式。 下表标识基于所用存储模式的备份的信息。  
  
|存储模式|备份的信息|  
|------------------|-----------------------------------|  
|多维 OLAP (MOLAP)|源数据、聚合和元数据|  
|混合 OLAP (HOLAP)|聚合和元数据|  
|关系 OLAP (ROLAP)|元数据|  
  
 期间`Backup`命令时，共享的锁置于[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库`Object`元素。 后释放共享的锁`Backup`命令是否已完成。  
  
 多个`Backup`命令可以并行运行，如果命令包含在[并行](../xml-elements-properties/parallel-element-xmla.md)的集合[批处理](batch-element-xmla.md)命令。 `Parallel` 集合可以使数据库同时备份到多个备份文件中。  
  
 有关备份和还原数据库的详细信息，请参阅[备份、 还原和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行备份命令的用户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
## <a name="see-also"></a>请参阅  
 [Restore 元素&#40;XMLA&#41;](restore-element-xmla.md)   
 [Synchronize 元素&#40;XMLA&#41;](synchronize-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
