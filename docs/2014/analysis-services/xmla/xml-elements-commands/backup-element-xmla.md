---
title: 备份元素 (XMLA) |Microsoft 文档
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
caps.latest.revision: 19
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: bd1f2317c28acd2e6037520334168491ec0bbcbe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138926"
---
# <a name="backup-element-xmla"></a>Backup 元素 (XMLA)
  备份[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]到备份文件的数据库。  
  
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
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md)， [ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md)， [BackupRemotePartitions](../xml-elements-properties/backupremotepartitions-element-xmla.md)，[文件](../xml-elements-properties/file-element-xmla.md)，[位置](../xml-elements-properties/locations-element-xmla.md)， [对象](../xml-elements-properties/object-element-xmla.md)，[密码](../xml-elements-properties/password-element-xmla.md)，[安全](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Backup`命令备份[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库[对象](../xml-elements-properties/object-element-xmla.md)备份文件，或者备份到远程备份文件的远程分区的元素。 如果 `Object` 元素指向非 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库对象，则会出错。  
  
 哪些信息`Backup`备份取决于数据库中的对象所使用的存储模式的命令。 下表标识基于所用存储模式的备份的信息。  
  
|存储模式|备份的信息|  
|------------------|-----------------------------------|  
|多维 OLAP (MOLAP)|源数据、聚合和元数据|  
|混合 OLAP (HOLAP)|聚合和元数据|  
|关系 OLAP (ROLAP)|元数据|  
  
 期间`Backup`命令时，在上放置共享的锁[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库`Object`元素。 后释放共享的锁`Backup`命令已完成。  
  
 多个`Backup`命令可以并行运行的如果命令包括在[并行](../xml-elements-properties/parallel-element-xmla.md)集合[批处理](batch-element-xmla.md)命令。 `Parallel` 集合可以使数据库同时备份到多个备份文件中。  
  
 有关备份和还原数据库的详细信息，请参阅[Backing Up、 正在还原，和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行备份命令的用户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
## <a name="see-also"></a>请参阅  
 [Restore 元素&#40;XMLA&#41;](restore-element-xmla.md)   
 [同步元素&#40;XMLA&#41;](synchronize-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  