---
title: "ObjectTypeEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8eb88d7f3df60d8c54782d20af73e3fd5e917db3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="objecttypeenum"></a>ObjectTypeEnum
指定为其设置权限或所有权的数据库对象的类型。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|对象是列。|  
|**adPermObjDatabase**|3|对象是一个数据库。|  
|**adPermObjProcedure**|4|对象是一个过程。|  
|**adPermObjProviderSpecific**|-1|对象是由提供程序定义的类型。 如果出现错误，将*ObjectType*参数是**adPermObjProviderSpecific**和*ObjectTypeId*未提供。|  
|**adPermObjTable**|1|对象是一个表。|  
|**adPermObjView**|5|对象是一个视图。|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|

