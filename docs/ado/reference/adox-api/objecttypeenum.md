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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed7273b2fd24690956fa5c5ffe317ad9c00c40ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710265"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
指定要为其设置权限或所有权的数据库对象的类型。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|对象为一个列。|  
|**adPermObjDatabase**|3|该对象是一个数据库。|  
|**adPermObjProcedure**|4|该对象是一个过程。|  
|**adPermObjProviderSpecific**|-1|对象是由提供程序定义的类型。 如果将会出错*ObjectType*参数是**adPermObjProviderSpecific**和一个*ObjectTypeId*未提供。|  
|**adPermObjTable**|1|该对象是一个表。|  
|**adPermObjView**|5|该对象是视图。|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
