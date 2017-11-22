---
title: "ConnectPromptEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ConnectPromptEnum
helpviewer_keywords: ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dbb4f3f854f319d31f91f8e7f0d8a15cf4263495
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定是否应显示一个对话框，打开与数据源的连接时提示输入缺少的参数。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|始终提示。|  
|**adPromptComplete**|2|如果需要更多信息时将提示。|  
|**adPromptCompleteRequired**|3|如果详细的信息是必需的但不是允许将可选参数，则将提示。|  
|**adPromptNever**|4|永远不会提示。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>适用范围  
 [Prompt 属性 - 动态 (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
