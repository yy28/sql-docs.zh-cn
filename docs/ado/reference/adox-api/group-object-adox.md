---
title: 组对象 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8f11fb5e227b5b6ebd418775247756da55c359af
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712079"
---
# <a name="group-object-adox"></a>组对象 (ADOX)
表示具有受保护的数据库中的访问权限的组帐户。  
  
## <a name="remarks"></a>备注  
 [组](../../../ado/reference/adox-api/groups-collection-adox.md)系列[目录](../../../ado/reference/adox-api/catalog-object-adox.md)表示目录的所有组帐户。 **组**集合[用户](../../../ado/reference/adox-api/user-object-adox.md)表示只有该用户所属的组。  
  
 使用属性、 集合和方法**组**对象，你可以：  
  
-   标识与组[名称](../../../ado/reference/adox-api/name-property-adox.md)属性。  
  
-   确定是否一个组拥有读取、 写入或删除的权限[GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md)并[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)方法。  
  
-   访问的组中具有成员身份的用户帐户[用户](../../../ado/reference/adox-api/users-collection-adox.md)集合。  
  
-   访问特定于提供程序的属性与[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 本部分包含以下主题。  
  
-   [组对象属性、方法和事件](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
