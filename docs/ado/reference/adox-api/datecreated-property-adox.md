---
description: DateCreated 属性 (ADOX)
title: DateCreated 属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 46b94255726bde107e52b6ca9c3546b9744b4a9f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984748"
---
# <a name="datecreated-property-adox"></a>DateCreated 属性 (ADOX)
指示对象的创建日期。  
  
## <a name="return-values"></a>返回值  
 返回指定创建日期的 **变量** 值。 如果提供程序不支持 **DateCreated** ，则该值为 null。  
  
## <a name="remarks"></a>注解  
 新追加的对象的 **DateCreated** 属性为 null。 追加新的[视图](./view-object-adox.md)或[过程](./procedure-object-adox.md)之后，必须调用[视图](./views-collection-adox.md)或[过程](./procedures-collection-adox.md)集合的[Refresh](../ado-api/refresh-method-ado.md)方法，以获取**DateCreated**属性的值。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [过程对象 (ADOX)](./procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [表对象 (ADOX)](./table-object-adox.md)  
    :::column-end:::
    :::column:::
        [视图对象 (ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [DateCreated 和 DateModified 属性示例 (VB) ](./datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified 属性 (ADOX)](./datemodified-property-adox.md)