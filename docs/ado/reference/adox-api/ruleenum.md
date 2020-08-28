---
description: RuleEnum
title: RuleEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 66367d872e27629f1bf437961b99908d0c42e9f2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983368"
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