---
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
ms.openlocfilehash: c04bbd079de68891cf271ff2ea668696e29a4394
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762798"
---
# <a name="ruleenum"></a>RuleEnum
指定删除[密钥](../../../ado/reference/adox-api/key-object-adox.md)时要遵循的规则。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|级联更改。|  
|**adRINone**|0|默认。 不执行任何操作。|  
|**adRISetDefault**|3|"外键值" 设置为默认值。|  
|**adRISetNull**|2|外键值设置为 null。|  
  
## <a name="applies-to"></a>应用于  
 [DeleteRule 属性 (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
