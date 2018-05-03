---
title: GetPermissions 方法 (ADOX) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6520df4df486baed3feb859ede760049923a6eba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getpermissions-method-adox"></a>GetPermissions 方法 (ADOX)
返回的权限[组](../../../ado/reference/adox-api/group-object-adox.md)或[用户](../../../ado/reference/adox-api/user-object-adox.md)对象或对象容器上。  
  
## <a name="syntax"></a>语法  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>返回值  
 返回**长**值，该值指定该位掩码包含组或用户具有对对象的权限。 此值可为一个或多个[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常量。  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 A **Variant**值，该值指定为其设置权限对象的名称。 设置*名称*为 null 的值，如果你想要获取对象容器的权限。  
  
 *ObjectType*  
 A**长**值可以是之一的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常量，用于指定要为其获取权限对象的类型。  
  
 *ObjectTypeId*  
 選擇性。 A **Variant** OLE DB 规范所定义值，该值未指定提供程序对象类型的 GUID。 此参数是必需的如果*ObjectType*设置为**adPermObjProviderSpecific**; 否则为不使用它。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[组对象 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>另请参阅  
 [GetPermissions 和 SetPermissions 方法示例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name 属性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
