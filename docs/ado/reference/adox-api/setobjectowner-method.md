---
title: "SetObjectOwner 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Catalog::SetObjectOwner
- _Catalog::raw_SetObjectOwner
helpviewer_keywords:
- SetObjectOwner method [ADOX]
ms.assetid: e5170a37-9d6e-43db-bfb6-9b6631fa3048
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33226468d9d1f556d2cf7ec3edac37375b0c8d84
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setobjectowner-method"></a>SetObjectOwner 方法
指定中的某个对象的所有者[目录](../../../ado/reference/adox-api/catalog-object-adox.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parameters  
 *ObjectName*  
 A**字符串**值，该值指定要为其指定所有者对象的名称。  
  
 *ObjectType*  
 A**长**值可以是之一的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)指定的所有者类型的常量。  
  
 *OwnerName*  
 A**字符串**值，该值指定[名称](../../../ado/reference/adox-api/name-property-adox.md)的[用户](../../../ado/reference/adox-api/user-object-adox.md)或[组](../../../ado/reference/adox-api/group-object-adox.md)以拥有的对象。  
  
 *ObjectTypeId*  
 可选。 A **Variant**值，该值指定不由 OLE DB 规范定义的提供程序对象类型的 GUID。 此参数是必需的如果*ObjectType*设置为**adPermObjProviderSpecific**; 否则为不使用它。  
  
## <a name="remarks"></a>注释  
 如果提供程序不支持指定的对象所有者，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [GetObjectOwner 和 SetObjectOwner 方法示例 (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)
