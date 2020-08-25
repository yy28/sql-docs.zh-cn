---
description: 用户集合 (ADOX)
title: 用户集合 (ADOX) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0d452075b3659d3ad01ba28540217b8447950084
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769036"
---
# <a name="users-collection-adox"></a>用户集合 (ADOX)
包含[目录](./catalog-object-adox.md)或[组](./group-object-adox.md)的所有存储的[用户](./user-object-adox.md)对象。  
  
## <a name="remarks"></a>备注  
 [目录](./catalog-object-adox.md)的**用户**集合表示所有目录的用户。 [组](./group-object-adox.md)的**用户**集合仅表示在特定组中具有成员身份的用户。  
  
 **用户**集合的[APPEND](./append-method-adox-users.md)方法对于 ADOX 是唯一的。 方法：  
  
-   使用 **Append** 方法将新用户添加到集合。  
  
 其余属性和方法对于 ADO 集合是标准的。 方法：  
  
-   使用 [Item](../ado-api/item-property-ado.md) 属性访问集合中的用户。  
  
-   返回集合中包含 [Count](../ado-api/count-property-ado.md) 属性的用户的数量。  
  
-   使用 [Delete](./delete-method-adox-collections.md) 方法从集合中删除用户。  
  
-   更新集合中的对象，以反映包含 [Refresh](../ado-api/refresh-method-ado.md) 方法的当前数据库的架构。  
  
> [!NOTE]
>  将**用户**对象追加到**组**对象**的用户**集合之前，**目录**的**用户**集合中必须已经存在与要追加的用户[对象同名的](./name-property-adox.md)**用户**对象。  
  
 本部分包含以下主题。  
  
-   [用户集合属性、方法和事件](./users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [GetPermissions 和 SetPermissions 方法示例 (VB) ](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [目录对象 (ADOX) ](./catalog-object-adox.md)   
 [用户对象 (ADOX)](./user-object-adox.md)