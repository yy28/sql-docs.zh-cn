---
description: ConnectPromptEnum
title: ConnectPromptEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ad8fe77bb3472931d3b16d5849b047001922c96
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444409"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定在打开与数据源的连接时是否应显示一个对话框，以提示输入缺少的参数。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|始终提示。|  
|**adPromptComplete**|2|如果需要详细信息，请提示。|  
|**adPromptCompleteRequired**|3|如果需要详细信息但不允许使用可选参数，则会提示。|  
|**adPromptNever**|4|从不提示。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums. ConnectPrompt. ALWAYS|  
|AdoEnums. ConnectPrompt. 完成|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums. ConnectPrompt. 从不|  
  
## <a name="applies-to"></a>适用于  
 [Prompt 属性 - 动态 (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
