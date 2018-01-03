---
title: "用户集合 (ADOX) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords: Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84e4484d2902913be2cf2afa615a474aeb2b4bf7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="users-collection-adox"></a>用户集合 (ADOX)
包含所有存储[用户](../../../ado/reference/adox-api/user-object-adox.md)的对象[目录](../../../ado/reference/adox-api/catalog-object-adox.md)或[组](../../../ado/reference/adox-api/group-object-adox.md)。  
  
## <a name="remarks"></a>Remarks  
 **用户**集合[目录](../../../ado/reference/adox-api/catalog-object-adox.md)表示目录的所有用户。 **用户**集合[组](../../../ado/reference/adox-api/group-object-adox.md)表示仅限拥有特定的组成员身份的用户。  
  
 [追加](../../../ado/reference/adox-api/append-method-adox-users.md)方法**用户**集合是唯一的 ADOX。 您可以：  
  
-   通过将新用户添加到集合**追加**方法。  
  
 剩余的属性和方法是标准到 ADO 集合。 您可以：  
  
-   访问集合中具有用户[项](../../../ado/reference/ado-api/item-property-ado.md)属性。  
  
-   返回与集合中包含的用户数[计数](../../../ado/reference/ado-api/count-property-ado.md)属性。  
  
-   从集合中删除用户[删除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映当前数据库的架构集合中的对象[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
> [!NOTE]
>  在追加之前**用户**对象传递给**用户**集合**组**对象，**用户**对象具有相同[名称](../../../ado/reference/adox-api/name-property-adox.md)如要追加的一个必须已存在于**用户**集合**目录**。  
  
 本部分包含以下主题。  
  
-   [用户集合属性、方法和事件](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [GetPermissions 和 SetPermissions 方法示例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
