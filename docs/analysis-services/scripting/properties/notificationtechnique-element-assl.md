---
title: "NotificationTechnique 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: NotificationTechnique Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: NotificationTechnique element
ms.assetid: 80c43de3-f147-4bf5-bb85-da9d182ce415
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 77b14f2946b6114e38755827f18ec2ff3eda5d7e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="notificationtechnique-element-assl"></a>NotificationTechnique 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]指定是否[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或外部的客户端应用程序处理的通知。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCachingBinding>  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*客户端*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*客户端*|由外部客户端应用程序处理通知。|  
|*Server*|由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 处理通知。|  
  
 对应于的父元素**NotificationTechnique**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ProactiveCachingBinding>。  
  
 对应于的允许值为枚举**NotificationTechnique**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.NotificationTechnique>。  
  
## <a name="see-also"></a>另请参阅  
 [ProactiveCachingBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)  
  
  
