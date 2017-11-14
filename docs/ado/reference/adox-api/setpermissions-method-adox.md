---
title: "SetPermissions 方法 (ADOX) |Microsoft 文档"
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
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e830221fab599ace1304fb50ad8b0b22824e2bed
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setpermissions-method-adox"></a>SetPermissions 方法 (ADOX)
指定的权限[组](../../../ado/reference/adox-api/group-object-adox.md)或[用户](../../../ado/reference/adox-api/user-object-adox.md)对象上。  
  
## <a name="syntax"></a>语法  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 A**字符串**值，该值指定为其设置权限对象的名称。  
  
 *ObjectType*  
 A**长**值可以是之一的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常量，用于指定要为其获取权限对象的类型。  
  
 *操作*  
 A**长**值可以是之一的[ActionEnum](../../../ado/reference/adox-api/actionenum.md)指定要设置权限时执行的操作类型的常量。  
  
 *权限*  
 A**长**值可以是一个位屏蔽的一个或多个[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常量，指示设置的权限。  
  
 *继承*  
 可选。 A**长**值可以是之一的[InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md)常量，用于指定如何将对象将继承这些权限。 默认值是**adInheritNone**。  
  
 *ObjectTypeId*  
 可选。 A **Variant**值，该值指定不由 OLE DB 规范定义的提供程序对象类型的 GUID。 此参数是必需的如果*ObjectType*设置为**adPermObjProviderSpecific**; 否则为不使用它。  
  
## <a name="remarks"></a>注释  
 如果提供程序不支持组或用户的设置访问权限，将会出错。  
  
> [!NOTE]
>  在调用时**SetPermissions**，将操作设置为**adAccessRevoke**替代的任何设置*权限*参数。 未设置*操作*到**adAccessRevoke**如果你想中指定的权限*权限*参数才会生效。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[组对象 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>另请参阅  
 [GetPermissions 和 SetPermissions 方法示例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name 属性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)

