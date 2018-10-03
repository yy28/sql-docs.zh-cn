---
title: Restore 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df3e4814b0dafadd8ba7a5c6f572fba7d48e6d4a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094657"
---
# <a name="restore-element-xmla"></a>Restore 元素 (XMLA)
  还原[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库从备份文件。  
  
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
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md)， [DatabaseName](../xml-elements-properties/name-element-xmla.md)， [DatabaseID](../xml-elements-properties/id-element-xmla.md)，[文件](../xml-elements-properties/file-element-xmla.md)，[位置](../xml-elements-properties/locations-element-xmla.md)，[密码](../xml-elements-properties/password-element-xmla.md)，[安全](../xml-elements-properties/security-element-xmla.md)， [DbStorageLocation](../xml-elements-properties/dbstoragelocation-element.md)|  
  
## <a name="remarks"></a>备注  
 `Restore`命令还原[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库`DatabaseName`从备份文件和 （可选） 从远程备份文件还原远程分区的元素。  
  
 根据备份文件中存储的对象使用的存储模式`Restore`命令还原下表中列出的信息。  
  
|存储模式|信息|  
|------------------|-----------------|  
|多维 OLAP (MOLAP)|源数据、聚合和元数据|  
|混合 OLAP (HOLAP)|聚合和元数据|  
|关系 OLAP (ROLAP)|元数据|  
  
 期间`Restore`命令时，排他锁置于[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库`DatabaseName`元素。 该锁被释放后`Restore`命令是否已完成。  
  
 有关备份和还原数据库的详细信息，请参阅[备份、 还原和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
## <a name="see-also"></a>请参阅  
 [备份元素&#40;XMLA&#41;](backup-element-xmla.md)   
 [批处理元素&#40;XMLA&#41;](batch-element-xmla.md)   
 [并行元素&#40;XMLA&#41;](../xml-elements-properties/parallel-element-xmla.md)   
 [Synchronize 元素&#40;XMLA&#41;](synchronize-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
