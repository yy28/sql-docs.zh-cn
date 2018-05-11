---
title: 版本元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0d6a79d53fa84f42d80924ab7246f42ca8057e6f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="edition-element-assl"></a>Edition 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的实例的只读版本[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]由[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Server>  
      ...  
      <Edition>...</Edition>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **版本**元素描述的是哪个版本[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]安装。 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*Standard*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用于 32 位处理器的 standard edition。|  
|*企业*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 32 位处理器的 Enterprise edition。|  
|*EnterpriseCore*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition： 基于内核授予许可。 32 位处理器。|  
|*BusinessIntelligence*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 32 位处理器的 business Intelligence edition。|  
|*开发人员*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 32 位处理器的开发人员版|  
|*评估*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 64 位处理器的评估版。|  
|*本地*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本地版本进行 32 位处理器。|  
|*Standard64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用于 64 位处理器的 standard edition。|  
|*Enterprise64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition 64 位处理器。|  
|*EnterpriseCore64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition： 基于内核授予许可。 64 位处理器。|  
|*BusinessIntelligence64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence edition 64 位处理器。|  
|*Developer64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 64 位处理器的开发人员版|  
|*Evaluation64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 64 位处理器的评估版。|  
|*Local64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本地版本进行 64 位处理器。|  
  
 对应的允许值为枚举**服务器版**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ServerEdition>。  
  
## <a name="see-also"></a>另请参阅  
 [版本元素 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/version-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
