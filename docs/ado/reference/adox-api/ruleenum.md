---
description: RuleEnum
title: RuleEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RuleEnum
helpviewer_keywords:
- RuleEnum enumeration [ADOX]
ms.assetid: 738fd3ff-3daf-483d-a0b9-88bef1be54c1
author: rothja
ms.author: jroth
ms.openlocfilehash: da49bbacf8ba59ba12f59fb072e9b5ec8c2ec2ea
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769456"
---
# <a name="ruleenum"></a>RuleEnum
指定删除 [密钥](./key-object-adox.md) 时要遵循的规则。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|级联更改。|  
|**adRINone**|0|默认。 不执行任何操作。|  
|**adRISetDefault**|3|"外键值" 设置为默认值。|  
|**adRISetNull**|2|外键值设置为 null。|  
  
## <a name="applies-to"></a>适用于  
 [DeleteRule 属性 (ADOX)](./deleterule-property-adox.md)