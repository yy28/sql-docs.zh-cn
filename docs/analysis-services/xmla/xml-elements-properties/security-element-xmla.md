---
title: 安全元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e9cbdf67846956a504e86245cb9532d40d7c016b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="security-element-xmla"></a>Security 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指定如何备份或还原期间安全定义，如角色和权限，[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)或[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Security>...</Security>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*skipMembership*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **安全**元素确定的安全定义，如角色和权限，是否定义上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库，备份或还原期间，分别**备份**或**还原**命令。 此元素还确定是否的一部分包括的 Windows 用户帐户和组定义为安全定义的成员**备份**或**还原**命令。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*skipMembership*|包含安全定义，但排除成员身份信息期间**备份**或**还原**命令。|  
|*CopyAll*|包含安全定义和成员身份信息期间**备份**或**还原**命令。|  
|*IgnoreSecurity*|排除期间安全定义**备份**或**还原**命令。|  
  
## <a name="see-also"></a>另请参阅  
 [SynchronizeSecurity 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
