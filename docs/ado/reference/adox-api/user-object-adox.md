---
title: 用户对象 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6fb3ebf1921bf0e61fe9d5a8dcf9fc2cd0dce6c1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705642"
---
# <a name="user-object-adox"></a>用户对象 (ADOX)
表示具有受保护的数据库中的访问权限的用户帐户。  
  
## <a name="remarks"></a>备注  
 [用户](../../../ado/reference/adox-api/users-collection-adox.md)系列[目录](../../../ado/reference/adox-api/catalog-object-adox.md)表示目录的所有用户。 **用户**集合[组](../../../ado/reference/adox-api/group-object-adox.md)表示只有特定组的用户。  
  
 使用属性、 集合和方法**用户**对象，你可以：  
  
-   标识与用户[名称](../../../ado/reference/adox-api/name-property-adox.md)属性。  
  
-   更改具有的用户的密码[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法。  
  
-   确定用户是否具有读取、 写入或删除的权限[GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md)并[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)方法。  
  
-   访问用户所属的组[组](../../../ado/reference/adox-api/groups-collection-adox.md)集合。  
  
-   访问特定于提供程序的属性与[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
-   确定[ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md)用户。  
  
 本部分包含以下主题。  
  
-   [用户对象属性、方法和事件](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [GetPermissions 和 SetPermissions 方法示例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
