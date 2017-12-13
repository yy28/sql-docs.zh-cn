---
title: "Restore 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
apiname: Restore Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Restore
- urn:schemas-microsoft-com:xml-analysis#Restore
- microsoft.xml.analysis.restore
helpviewer_keywords: Restore command
ms.assetid: bb5a0c92-3927-4fa4-975b-6e4d79e0a912
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4459dbc293759ffbfa5ac9c32fa910cd31deaae3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="restore-element-xmla"></a>Restore 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]还原[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]从备份文件的数据库。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)， [DatabaseName](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md)， [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md)，[文件](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)，[密码](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)，[安全](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)， [DbStorageLocation](../../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)|  
  
## <a name="remarks"></a>注释  
 **还原**命令还原[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库**DatabaseName**从备份文件和 （可选） 从远程备份文件还原远程分区的元素。  
  
 根据备份文件中存储的对象所使用的存储模式， **Restore** 命令还原下表中列出的信息。  
  
|存储模式|信息|  
|------------------|-----------------|  
|多维 OLAP (MOLAP)|源数据、聚合和元数据|  
|混合 OLAP (HOLAP)|聚合和元数据|  
|关系 OLAP (ROLAP)|元数据|  
  
 期间**还原**命令时，排他锁所在[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定数据库**DatabaseName**元素。 排他锁会在 **Restore** 命令完成后释放。  
  
 有关备份和还原数据库的详细信息，请参阅[Backing Up，正在还原，和同步数据库 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
## <a name="see-also"></a>另请参阅  
 [Backup 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [Batch 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Parallel 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)   
 [同步元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
