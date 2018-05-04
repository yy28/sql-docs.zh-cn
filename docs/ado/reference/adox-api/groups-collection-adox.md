---
title: 组集合 (ADOX) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c98bb6f455878df0605d1e7f7c9fc1d9554a1cb8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="groups-collection-adox"></a>组集合 (ADOX)
包含所有存储[组](../../../ado/reference/adox-api/group-object-adox.md)目录或用户的对象。  
  
## <a name="remarks"></a>注释  
 **组**集合[目录](../../../ado/reference/adox-api/catalog-object-adox.md)表示所有目录的组帐户。 **组**集合[用户](../../../ado/reference/adox-api/user-object-adox.md)表示仅用户所属的组。  
  
 [追加](../../../ado/reference/adox-api/append-method-adox-groups.md)方法**组**集合是唯一的 ADOX。 您可以：  
  
-   将新的安全组添加到具有集合**追加**方法。  
  
 剩余的属性和方法是标准到 ADO 集合。 您可以：  
  
-   访问集合中具有一组[项](../../../ado/reference/ado-api/item-property-ado.md)属性。  
  
-   返回与集合中包含的组数[计数](../../../ado/reference/ado-api/count-property-ado.md)属性。  
  
-   从集合中删除组[删除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映当前的数据库架构和集合中的对象[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
> [!NOTE]
>  在追加之前**组**对象传递给**组**集合**用户**对象，**组**对象具有相同[名称](../../../ado/reference/adox-api/name-property-adox.md)如要追加的一个必须已存在于**组**集合**目录**。  
  
 本部分包含以下主题。  
  
-   [组集合属性、方法和事件](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [组对象 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
