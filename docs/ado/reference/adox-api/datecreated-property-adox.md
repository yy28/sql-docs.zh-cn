---
description: DateCreated 属性 (ADOX)
title: DateCreated 属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
author: rothja
ms.author: jroth
ms.openlocfilehash: 37101d33e8a0efcda56dae5df13d7afd299f6f23
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440159"
---
# <a name="datecreated-property-adox"></a>DateCreated 属性 (ADOX)
指示对象的创建日期。  
  
## <a name="return-values"></a>返回值  
 返回指定创建日期的 **变量** 值。 如果提供程序不支持 **DateCreated** ，则该值为 null。  
  
## <a name="remarks"></a>备注  
 新追加的对象的 **DateCreated** 属性为 null。 追加新的[视图](../../../ado/reference/adox-api/view-object-adox.md)或[过程](../../../ado/reference/adox-api/procedure-object-adox.md)之后，必须调用[视图](../../../ado/reference/adox-api/views-collection-adox.md)或[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)集合的[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，以获取**DateCreated**属性的值。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
    :::column-end:::
    :::column:::
        [视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [DateCreated 和 DateModified 属性示例 (VB) ](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified 属性 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
