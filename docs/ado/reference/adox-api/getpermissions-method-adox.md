---
title: GetPermissions 方法 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f5b2a5170b499f5e88d4caac4822d2998691eea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966223"
---
# <a name="getpermissions-method-adox"></a>GetPermissions 方法 (ADOX)
返回的权限[组](../../../ado/reference/adox-api/group-object-adox.md)或[用户](../../../ado/reference/adox-api/user-object-adox.md)对象或对象容器。  
  
## <a name="syntax"></a>语法  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>返回值  
 返回**长**值，该值指定该位掩码包含组或用户具有对对象的权限。 此值可以是一种或多种[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常量。  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 一个**变体**值，该值指定要为其设置权限的对象的名称。 设置*名称*为 null 的值，如果你想要获取对象容器的权限。  
  
 *ObjectType*  
 一个**长**值，它可以是其中一个的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常量，指定要为其获取权限的对象类型。  
  
 *ObjectTypeId*  
 可选。 一个**变体**由 OLE DB 规范定义的值，该值未指定提供程序对象类型的 GUID。 此参数是必需的如果*ObjectType*设置为**adPermObjProviderSpecific**; 否则为不使用它。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[组对象 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>请参阅  
 [GetPermissions 和 SetPermissions 方法示例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name 属性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
