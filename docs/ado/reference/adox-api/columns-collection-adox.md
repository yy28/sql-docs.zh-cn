---
title: 列集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
author: rothja
ms.author: jroth
ms.openlocfilehash: 46168e694f87c4a8a827420f8b395b843da1d29b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759333"
---
# <a name="columns-collection-adox"></a>列集合 (ADOX)
包含表、索引或键的所有[列](../../../ado/reference/adox-api/column-object-adox.md)对象。  
  
## <a name="remarks"></a>备注  
 **列**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-columns.md)方法对于 ADOX 是唯一的。 你可以：  
  
-   使用**Append**方法向集合中添加一个新列。  
  
 其余属性和方法对于 ADO 集合是标准的。 你可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)属性访问集合中的列。  
  
-   返回集合中包含的[Count](../../../ado/reference/ado-api/count-property-ado.md)属性的列数。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法从集合中删除列。  
  
-   更新集合中的对象，以反映包含[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法的当前数据库的架构。  
  
> [!NOTE]
>  如果**列**不存在于已追加到[Tables](../../../ado/reference/adox-api/tables-collection-adox.md)集合的[表](../../../ado/reference/adox-api/table-object-adox.md)中，则当向[索引](../../../ado/reference/adox-api/index-object-adox.md)的**Columns**集合追加**列**时，将发生错误。  
  
 本部分包含以下主题。  
  
-   [列集合属性、方法和事件](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [列和表追加方法，Name 属性示例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [连接关闭方法，表类型属性示例（VB）](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 属性示例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 属性示例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 属性示例（VB）](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [列对象 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
