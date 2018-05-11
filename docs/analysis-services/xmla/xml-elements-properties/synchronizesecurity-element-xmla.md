---
title: SynchronizeSecurity 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f2fe0ffd1e2cd331228d72832ee5c6368bd27d4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="synchronizesecurity-element-xmla"></a>SynchronizeSecurity 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指定如何将安全定义，如角色和权限，同步期间[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Synchronize>  
   ...  
   <SynchronizeSecurity>...</SynchronizeSecurity>  
   ...  
</Synchronize>  
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
|父元素|[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **安全**元素确定的安全定义，如角色和权限，是否定义上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库同步期间**同步**命令。 此元素还确定是否的一部分包括的 Windows 用户帐户和组定义为安全定义的成员**同步**命令。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*skipMembership*|包含安全定义，但排除成员身份信息期间**同步**命令。|  
|*CopyAll*|包含安全定义和成员身份信息期间**同步**命令。|  
|*IgnoreSecurity*|排除期间安全定义**同步**命令。|  
  
## <a name="see-also"></a>另请参阅  
 [安全元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
