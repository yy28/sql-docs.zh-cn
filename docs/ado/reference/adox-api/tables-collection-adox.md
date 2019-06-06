---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1ba06c10b3f890f08abac371346c3d03a0278aa8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705723"
---
# <a name="tables-collection-adox"></a>表集合 (ADOX)
包含所有[表](../../../ado/reference/adox-api/table-object-adox.md)的目录对象。  
  
## <a name="remarks"></a>备注  
 [追加](../../../ado/reference/adox-api/append-method-adox-tables.md)方法**表**是唯一的 ADOX 集合。 您可以：  
  
-   将新表添加到具有集合**追加**方法。  
  
 剩余的属性和方法是标准到 ADO 集合。 您可以：  
  
-   访问集合中具有表[项](../../../ado/reference/ado-api/item-property-ado.md)属性。  
  
-   返回与集合中包含的表数[计数](../../../ado/reference/ado-api/count-property-ado.md)属性。  
  
-   从集合中删除表[删除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映与当前的数据库架构集合中的对象[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
 某些提供程序可能返回其他架构对象，一个视图，如**表**集合。 因此，某些 ADOX 集合可能包含多个引用同一对象。 你应从一个集合中删除对象，更改不会显示在另一个集合中引用已删除的对象，直到**刷新**在集合上调用方法。 例如，使用 OLE DB Provider for Microsoft Jet，视图将返回**表**集合。 如果您删除视图，则必须刷新**表**之前集合将反映此更改的集合。  
  
 本部分包含以下主题。  
  
-   [表集合属性、方法和事件](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [目录 ActiveConnection 属性示例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [列和表 Append 方法、 Name 属性示例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [连接的 Close 方法、 表 Type 属性示例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [项 Append 方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
