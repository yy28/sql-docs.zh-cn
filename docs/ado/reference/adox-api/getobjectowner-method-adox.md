---
title: GetObjectOwner 方法 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3b5ab8c21ee02f646bf4b8e4f4941fafd6edfde
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712126"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner 方法 (ADOX)
返回中的对象的所有者[目录](../../../ado/reference/adox-api/catalog-object-adox.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>返回值  
 返回**字符串**值，该值指定[名称](../../../ado/reference/adox-api/name-property-adox.md)的[用户](../../../ado/reference/adox-api/user-object-adox.md)或者[组](../../../ado/reference/adox-api/group-object-adox.md)拥有此对象。  
  
#### <a name="parameters"></a>Parameters  
 *ObjectName*  
 一个**字符串**值，该值指定要为其返回所有者对象的名称。  
  
 *ObjectType*  
 一个**长**值，它可以是其中一个的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常量，它指定要获取其所有者的对象的类型。  
  
 *ObjectTypeId*  
 可选。 一个**变体**由 OLE DB 规范定义的值，该值未指定提供程序对象类型的 GUID。 此参数是必需的如果*ObjectType*设置为**adPermObjProviderSpecific**; 否则为不使用它。  
  
## <a name="remarks"></a>备注  
 如果提供程序不支持返回对象的所有者，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [GetObjectOwner 和 SetObjectOwner 方法示例 (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)
