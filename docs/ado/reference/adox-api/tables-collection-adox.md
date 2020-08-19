---
description: 表集合 (ADOX)
title: 表集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
author: rothja
ms.author: jroth
ms.openlocfilehash: 9d959578d647e74248fdb58b8c27269c0454c304
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439469"
---
# <a name="tables-collection-adox"></a>表集合 (ADOX)
包含目录的所有 [表](../../../ado/reference/adox-api/table-object-adox.md) 对象。  
  
## <a name="remarks"></a>备注  
 **表**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-tables.md)方法对于 ADOX 是唯一的。 可以：  
  
-   使用 **Append** 方法向集合中添加一个新表。  
  
 其余属性和方法对于 ADO 集合是标准的。 可以：  
  
-   使用 [Item](../../../ado/reference/ado-api/item-property-ado.md) 属性访问集合中的表。  
  
-   返回集合中包含 [Count](../../../ado/reference/ado-api/count-property-ado.md) 属性的表的数目。  
  
-   使用 [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 方法从集合中删除一个表。  
  
-   更新集合中的对象，以反映包含 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 方法的当前数据库架构。  
  
 某些提供程序可能在 **Tables** 集合中返回其他架构对象，如视图。 因此，某些 ADOX 集合可能包含对同一对象的多个引用。 如果从一个集合中删除对象，则在对集合调用 **Refresh** 方法之前，将不会在引用该已删除对象的另一个集合中看到此更改。 例如，对于 Microsoft Jet 的 OLE DB 提供程序，视图将与 **Tables** 集合一起返回。 如果删除视图，则必须刷新 **表** 集合，然后集合才能反映此更改。  
  
 本部分包含以下主题。  
  
-   [表集合属性、方法和事件](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录 ActiveConnection 属性示例 (VB) ](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [列和表追加方法、Name 属性示例 (VB) ](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [连接关闭方法，表类型属性示例 (VB) ](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule Properties Example (VB) ](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [目录对象 (ADOX) ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
