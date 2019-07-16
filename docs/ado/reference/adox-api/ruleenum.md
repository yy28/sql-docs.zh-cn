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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87c61baa93cb1dbca58bbe86ffc254a92d2b9d5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965246"
---
# <a name="ruleenum"></a>RuleEnum
指定何时应遵循的规则[密钥](../../../ado/reference/adox-api/key-object-adox.md)被删除。  
  
|常量|值|描述|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|级联更改。|  
|**adRINone**|0|默认值。 不执行任何操作。|  
|**adRISetDefault**|3|外键的值设置为默认值。|  
|**adRISetNull**|2|外键的值设置为 null。|  
  
## <a name="applies-to"></a>适用范围  
 [DeleteRule 属性 (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
