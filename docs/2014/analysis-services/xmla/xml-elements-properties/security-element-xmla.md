---
title: 安全元素 (XMLA) |Microsoft 文档
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
- Security Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.security
- urn:schemas-microsoft-com:xml-analysis#Security
- http://schemas.microsoft.com/analysisservices/2003/engine#Security
helpviewer_keywords:
- Security element
ms.assetid: 0b601f69-d16d-4d10-9361-b8afaa6ed357
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4811ae03eb6f30c4b9f4557e791339920161b4ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138501"
---
# <a name="security-element-xmla"></a>Security 元素 (XMLA)
  指定如何备份或还原期间安全定义，如角色和权限，[备份](../xml-elements-commands/backup-element-xmla.md)或[还原](../xml-elements-commands/restore-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Security>...</Security>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*SkipMembership*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../xml-elements-commands/backup-element-xmla.md)，[还原](../xml-elements-commands/restore-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Security`元素确定的安全定义，如角色和权限，是否定义上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库是备份或还原期间，分别`Backup`或`Restore`命令。 此元素还确定定义为安全定义成员的 Windows 用户帐户和用户组是否包含在 `Backup` 或 `Restore` 命令中。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*SkipMembership*|执行 `Backup` 或 `Restore` 命令时，包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|执行 `Backup` 或 `Restore` 命令时，包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|执行 `Backup` 或 `Restore` 命令时，不包括安全定义。|  
  
## <a name="see-also"></a>请参阅  
 [SynchronizeSecurity 元素&#40;XMLA&#41;](security-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  