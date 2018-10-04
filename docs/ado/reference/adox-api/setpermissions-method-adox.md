---
title: SetPermissions 方法 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d3ff679af7a577433a8191d3beca10eed1d22cf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602417"
---
# <a name="setpermissions-method-adox"></a>SetPermissions 方法 (ADOX)
指定的权限[组](../../../ado/reference/adox-api/group-object-adox.md)或[用户](../../../ado/reference/adox-api/user-object-adox.md)对象上。  
  
## <a name="syntax"></a>语法  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 一个**字符串**值，该值指定要为其设置权限的对象的名称。  
  
 *ObjectType*  
 一个**长**值，它可以是其中一个的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常量，指定要为其获取权限的对象类型。  
  
 *操作*  
 一个**长**值，它可以是其中一个的[ActionEnum](../../../ado/reference/adox-api/actionenum.md)指定要设置权限时执行的操作类型的常量。  
  
 *权限*  
 一个**长**值，它可以是一个位掩码的一个或多个[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常量，指示要设置的权限。  
  
 *继承*  
 可选。 一个**长**值，它可以是其中一个的[InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md)常量，它指定如何对象将继承这些权限。 默认值是**adInheritNone**。  
  
 *ObjectTypeId*  
 可选。 一个**变体**值，该值指定未由 OLE DB 规范定义的提供程序对象类型的 GUID。 此参数是必需的如果*ObjectType*设置为**adPermObjProviderSpecific**; 否则为不使用它。  
  
## <a name="remarks"></a>备注  
 如果提供程序不支持设置访问权限的组或用户，将会出错。  
  
> [!NOTE]
>  调用时**SetPermissions**，将操作设置为**adAccessRevoke**重写的任何设置*Rights*参数。 未设置*操作*到**adAccessRevoke**如果你想中指定的权限*Rights*参数才能生效。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[组对象 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>请参阅  
 [GetPermissions 和 SetPermissions 方法示例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name 属性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
