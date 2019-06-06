---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40ce74748e15a2715de26e813007e00be0c33729
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698607"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定是否应显示一个对话框以打开与数据源的连接时提示输入缺少的参数。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|始终提示。|  
|**adPromptComplete**|2|如果需要更多的信息，提示。|  
|**adPromptCompleteRequired**|3|如果需要详细信息，但是不允许使用可选参数，则会提示。|  
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
