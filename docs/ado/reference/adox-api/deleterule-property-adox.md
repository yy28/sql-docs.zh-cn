---
description: DeleteRule 属性 (ADOX)
title: DeleteRule 属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Key::put_DeleteRule
- _Key::DeleteRule
- _Key::GetDeleteRule
- _Key::PutDeleteRule
- _Key::get_DeleteRule
helpviewer_keywords:
- DeleteRule property [ADOX]
ms.assetid: 87bd4c0a-cae3-4007-a939-4193acaa00ac
author: rothja
ms.author: jroth
ms.openlocfilehash: b25e0da0cc9fdbb622f3a844efa4c4ea784100be
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770586"
---
# <a name="deleterule-property-adox"></a>DeleteRule 属性 (ADOX)
指示在删除主键时执行的操作。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回一个 **Long** 值，该值可以是 [RuleEnum](./ruleenum.md) 常数之一。 默认值为 **adRINone**。  
  
## <a name="remarks"></a>备注  
 对于已追加到集合的 [键](./key-object-adox.md) 对象，此属性是只读的。  
  
## <a name="applies-to"></a>适用于  
 [项对象 (ADOX)](./key-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [DeleteRule 属性示例 (VB)](./deleterule-property-example-vb.md)