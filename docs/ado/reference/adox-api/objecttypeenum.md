---
description: ObjectTypeEnum
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
ms.openlocfilehash: f4d12a6f1a14374e19a816e70099901126fad5be
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769916"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
指定要为其设置权限或所有权的数据库对象的类型。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|对象是一个列。|  
|**adPermObjDatabase**|3|对象是数据库。|  
|**adPermObjProcedure**|4|对象是一个过程。|  
|**adPermObjProviderSpecific**|-1|对象是由提供程序定义的类型。 如果 *ObjectType* 参数为 **adPermObjProviderSpecific** 并且未提供 *ObjectTypeId* ，则会发生错误。|  
|**adPermObjTable**|1|对象是一个表。|  
|**adPermObjView**|5|对象是一个视图。|  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [GetObjectOwner 方法 (ADOX)](./getobjectowner-method-adox.md)  
        [GetPermissions 方法 (ADOX)](./getpermissions-method-adox.md)  
    :::column-end:::
    :::column:::
        [SetObjectOwner 方法](./setobjectowner-method.md)  
        [SetPermissions 方法 (ADOX)](./setpermissions-method-adox.md)  
    :::column-end:::
:::row-end:::