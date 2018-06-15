---
title: 表集合 (ADOX) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6b97d189907d8f226867748e25e64972b8aba2b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35287206"
---
# <a name="tables-collection-adox"></a>表集合 (ADOX)
包含所有[表](../../../ado/reference/adox-api/table-object-adox.md)的目录对象。  
  
## <a name="remarks"></a>Remarks  
 [追加](../../../ado/reference/adox-api/append-method-adox-tables.md)方法**表**集合是唯一的 ADOX。 您可以：  
  
-   将新表添加到具有集合**追加**方法。  
  
 剩余的属性和方法是标准到 ADO 集合。 您可以：  
  
-   访问集合中具有表[项](../../../ado/reference/ado-api/item-property-ado.md)属性。  
  
-   返回与集合中包含的表的数目[计数](../../../ado/reference/ado-api/count-property-ado.md)属性。  
  
-   从集合中删除表[删除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映当前的数据库架构和集合中的对象[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
 某些提供程序可能返回其他架构对象，如视图中**表**集合。 因此，某些 ADOX 集合可能包含对同一对象的多个引用。 你应从一个集合中删除对象，更改将不可见，引用已删除的对象，直到另一个集合中**刷新**集合上调用方法。 例如，与 OLE DB Provider for Microsoft Jet，视图将返回**表**集合。 如果您删除视图，则必须刷新**表**之前集合将反映这些更改的集合。  
  
 本部分包含以下主题。  
  
-   [表集合属性、方法和事件](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [目录 ActiveConnection 属性示例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [列和表追加方法名称的属性示例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [连接关闭方法，表类型的属性示例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [密钥追加方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
