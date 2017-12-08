---
title: "备份元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Backup Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Backup
- http://schemas.microsoft.com/analysisservices/2003/engine#Backup
- microsoft.xml.analysis.backup
helpviewer_keywords: Backup command
ms.assetid: 5bcbc14c-9db9-45b2-99de-f3a265bcb0c4
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ed85939848e2304cec9651245815c3848da5aa04
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)， [ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md)， [BackupRemotePartitions](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)，[文件](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)， [对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)，[密码](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)，[安全](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **备份**命令备份[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)备份文件，或者备份到远程备份文件的远程分区的元素。 如果**对象**元素而不引用的对象[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库，就会出错。  
  
 **Backup** 命令所备份的信息取决于数据库中对象所使用的存储模式。 下表标识基于所用存储模式的备份的信息。  
  
|存储模式|备份的信息|  
|------------------|-----------------------------------|  
|多维 OLAP (MOLAP)|源数据、聚合和元数据|  
|混合 OLAP (HOLAP)|聚合和元数据|  
|关系 OLAP (ROLAP)|元数据|  
  
 期间**备份**命令时，在上放置共享的锁[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库**对象**元素。 **Backup** 命令完成后释放共享锁。  
  
 多个**备份**命令可以并行运行的如果命令包括在[并行](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)集合[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令。 **Parallel** 集合可以使数据库同时备份到多个备份文件中。  
  
 有关备份和还原数据库的详细信息，请参阅[Backing Up，正在还原，和同步数据库 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行备份命令的用户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
## <a name="see-also"></a>另请参阅  
 [还原元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [同步元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
