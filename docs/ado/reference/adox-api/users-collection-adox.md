---
title: 用户集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a6146a942e572e28692ceaafd77d6958cdab9dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964954"
---
# <a name="users-collection-adox"></a>用户集合 (ADOX)
包含[目录](../../../ado/reference/adox-api/catalog-object-adox.md)或[组](../../../ado/reference/adox-api/group-object-adox.md)的所有存储的[用户](../../../ado/reference/adox-api/user-object-adox.md)对象。  
  
## <a name="remarks"></a>备注  
 [目录](../../../ado/reference/adox-api/catalog-object-adox.md)的**用户**集合表示所有目录的用户。 [组](../../../ado/reference/adox-api/group-object-adox.md)的**用户**集合仅表示在特定组中具有成员身份的用户。  
  
 **用户**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-users.md)方法对于 ADOX 是唯一的。 你可以：  
  
-   使用**Append**方法将新用户添加到集合。  
  
 其余属性和方法对于 ADO 集合是标准的。 你可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)属性访问集合中的用户。  
  
-   返回集合中包含[Count](../../../ado/reference/ado-api/count-property-ado.md)属性的用户的数量。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法从集合中删除用户。  
  
-   更新集合中的对象，以反映包含[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法的当前数据库的架构。  
  
> [!NOTE]
>  将**用户**对象追加到**组**对象**的用户**集合之前，**目录**的**用户**集合中必须已经存在与要追加的用户[对象同名的](../../../ado/reference/adox-api/name-property-adox.md)**用户**对象。  
  
 本部分包含以下主题。  
  
-   [用户集合属性、方法和事件](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [GetPermissions 和 SetPermissions 方法示例（VB）](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [目录对象（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
