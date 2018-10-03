---
title: 文件元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- File Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.file
- http://schemas.microsoft.com/analysisservices/2003/engine#File
- urn:schemas-microsoft-com:xml-analysis#File
helpviewer_keywords:
- File element
ms.assetid: 3dfd0e9b-746b-4ce5-8a95-610d2e573739
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a5ae3390405bc7a722934f3b3fb3652825b2ea03
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125447"
---
# <a name="file-element-xmla"></a>File 元素 (XMLA)
  标识的文件将由父[备份](../xml-elements-commands/backup-element-xmla.md)或[还原](../xml-elements-commands/restore-element-xmla.md)命令，或通过父[位置](location-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../xml-elements-commands/backup-element-xmla.md)，[位置](location-element-xmla.md)，[还原](../xml-elements-commands/restore-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `File` 元素包含一个 UNC 文件名，父元素确定 `File` 元素的用途。  
  
 对于 `Backup` 命令，`File` 元素确定 `Backup` 命令创建的备份文件的名称。 如果路径未指定文件名称的一部分，在指定的路径`BackupDir`的实例的配置属性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]使用。 如果指定的文件存在，除非将父 `AllowOverwrite` 命令的 `Backup` 元素设置为 `True`，否则将发生错误。  
  
 对于 `Restore` 命令，`File` 元素确定由 `Restore` 命令还原的备份文件的名称。  
  
 对于 `Location` 元素，`File` 元素介绍包含远程分区的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的远程备份文件。 有关备份和还原远程分区的详细信息，请参阅[备份、 还原和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [AllowOverwrite 元素&#40;XMLA&#41;](allowoverwrite-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
