---
title: Restore 元素 (XMLA) |Microsoft 文档
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
- Restore Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Restore
- urn:schemas-microsoft-com:xml-analysis#Restore
- microsoft.xml.analysis.restore
helpviewer_keywords:
- Restore command
ms.assetid: bb5a0c92-3927-4fa4-975b-6e4d79e0a912
caps.latest.revision: 26
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 0e8eca537c61be64de403b4ad08bb0e64040937c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129966"
---
# <a name="restore-element-xmla"></a>Restore 元素 (XMLA)
  还原[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]从备份文件的数据库。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Restore>  
      <DatabaseName>...</DatabaseName>  
      <DatabaseID>...</DatabaseID>  
      <File>...</File>  
      <Security>...</Security>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <Locations>...</Locations>  
      <DbStorageLocation>...</DbStorageLocation>  
   </Restore>  
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
|子元素|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md)， [DatabaseName](../xml-elements-properties/name-element-xmla.md)， [DatabaseID](../xml-elements-properties/id-element-xmla.md)，[文件](../xml-elements-properties/file-element-xmla.md)，[位置](../xml-elements-properties/locations-element-xmla.md)，[密码](../xml-elements-properties/password-element-xmla.md)，[安全](../xml-elements-properties/security-element-xmla.md)， [DbStorageLocation](../xml-elements-properties/dbstoragelocation-element.md)|  
  
## <a name="remarks"></a>Remarks  
 `Restore`命令还原[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库`DatabaseName`从备份文件和 （可选） 从远程备份文件还原远程分区的元素。  
  
 具体取决于在备份文件中，存储的对象所使用的存储模式`Restore`命令还原信息，如以下表中列出。  
  
|存储模式|信息|  
|------------------|-----------------|  
|多维 OLAP (MOLAP)|源数据、聚合和元数据|  
|混合 OLAP (HOLAP)|聚合和元数据|  
|关系 OLAP (ROLAP)|元数据|  
  
 期间`Restore`命令时，排他锁所在[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库`DatabaseName`元素。 该锁被释放后`Restore`命令已完成。  
  
 有关备份和还原数据库的详细信息，请参阅[Backing Up、 正在还原，和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
## <a name="see-also"></a>请参阅  
 [备份元素&#40;XMLA&#41;](backup-element-xmla.md)   
 [批处理元素&#40;XMLA&#41;](batch-element-xmla.md)   
 [并行元素&#40;XMLA&#41;](../xml-elements-properties/parallel-element-xmla.md)   
 [同步元素&#40;XMLA&#41;](synchronize-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  