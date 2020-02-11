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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965246"
---
# <a name="ruleenum"></a>RuleEnum
指定删除[密钥](../../../ado/reference/adox-api/key-object-adox.md)时要遵循的规则。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|级联更改。|  
|**adRINone**|0|默认值。 不执行任何操作。|  
|**adRISetDefault**|3|"外键值" 设置为默认值。|  
|**adRISetNull**|2|外键值设置为 null。|  
  
## <a name="applies-to"></a>应用于  
 [DeleteRule 属性 (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
