---
title: 组集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
author: rothja
ms.author: jroth
ms.openlocfilehash: e2b6e7b7669e0976cf47e5b4d5d2c827a824f919
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764848"
---
# <a name="groups-collection-adox"></a>组集合 (ADOX)
包含目录或用户的所有存储的[组](../../../ado/reference/adox-api/group-object-adox.md)对象。  
  
## <a name="remarks"></a>备注  
 [目录](../../../ado/reference/adox-api/catalog-object-adox.md)的**Groups**集合表示所有目录的组帐户。 [用户](../../../ado/reference/adox-api/user-object-adox.md)的**Groups**集合仅表示该用户所属的组。  
  
 **组**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-groups.md)方法对于 ADOX 是唯一的。 你可以：  
  
-   使用**Append**方法将新的安全组添加到集合。  
  
 其余属性和方法对于 ADO 集合是标准的。 你可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)属性访问集合中的组。  
  
-   返回集合中包含[Count](../../../ado/reference/ado-api/count-property-ado.md)属性的组的数目。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法从集合中删除组。  
  
-   更新集合中的对象，以反映包含[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法的当前数据库架构。  
  
> [!NOTE]
>  在将**组**对象追加到**用户**对象的**groups**集合之前，**目录**的**组**集合中必须已经存在与要追加的组[对象同名的](../../../ado/reference/adox-api/name-property-adox.md)**组**对象。  
  
 本部分包含以下主题。  
  
-   [组集合属性、方法和事件](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录对象（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [组对象 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
