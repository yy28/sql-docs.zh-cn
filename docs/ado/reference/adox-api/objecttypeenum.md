---
title: ObjectTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
author: rothja
ms.author: jroth
ms.openlocfilehash: fe7d97909a2d38e548a072245b08110b1d61eb3c
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86943159"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
指定要为其设置权限或所有权的数据库对象的类型。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|对象是一个列。|  
|**adPermObjDatabase**|3|对象是数据库。|  
|**adPermObjProcedure**|4|对象是一个过程。|  
|**adPermObjProviderSpecific**|-1|对象是由提供程序定义的类型。 如果*ObjectType*参数为**adPermObjProviderSpecific**并且未提供*ObjectTypeId* ，则会发生错误。|  
|**adPermObjTable**|1|对象是一个表。|  
|**adPermObjView**|5|对象是一个视图。|  
  
## <a name="applies-to"></a>应用到  

:::row:::
    :::column:::
        [GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)  
        [GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)  
    :::column-end:::
    :::column:::
        [SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)  
        [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)  
    :::column-end:::
:::row-end:::
