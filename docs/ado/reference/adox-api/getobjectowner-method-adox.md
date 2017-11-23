---
title: "GetObjectOwner 方法 (ADOX) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords: GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eb2c0957c4bda61387986eb1d05c4483954045ff
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner 方法 (ADOX)
返回中的某个对象的所有者[目录](../../../ado/reference/adox-api/catalog-object-adox.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>返回值  
 返回**字符串**值，该值指定[名称](../../../ado/reference/adox-api/name-property-adox.md)的[用户](../../../ado/reference/adox-api/user-object-adox.md)或[组](../../../ado/reference/adox-api/group-object-adox.md)拥有对象。  
  
#### <a name="parameters"></a>Parameters  
 *ObjectName*  
 A**字符串**值，该值指定为其返回的所有者的对象的名称。  
  
 *ObjectType*  
 A**长**值可以是之一的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常量，，指定要为其获取所有者的对象的类型。  
  
 *ObjectTypeId*  
 可选。 A **Variant** OLE DB 规范所定义值，该值未指定提供程序对象类型的 GUID。 此参数是必需的如果*ObjectType*设置为**adPermObjProviderSpecific**; 否则为不使用它。  
  
## <a name="remarks"></a>注释  
 如果提供程序不支持返回对象所有者，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [GetObjectOwner 和 SetObjectOwner 方法示例 (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)
