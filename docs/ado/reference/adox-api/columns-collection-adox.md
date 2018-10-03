---
title: 列集合 (ADOX) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5cd13809703c14022b6e2a1e7dbb87716c4778c9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600035"
---
# <a name="columns-collection-adox"></a>列集合 (ADOX)
包含所有[列](../../../ado/reference/adox-api/column-object-adox.md)表、 索引或键的对象。  
  
## <a name="remarks"></a>备注  
 [追加](../../../ado/reference/adox-api/append-method-adox-columns.md)方法**列**是唯一的 ADOX 集合。 您可以：  
  
-   将新列添加到具有集合**追加**方法。  
  
 剩余的属性和方法是标准到 ADO 集合。 您可以：  
  
-   访问集合中具有的列[项](../../../ado/reference/ado-api/item-property-ado.md)属性。  
  
-   返回与集合中包含的列数[计数](../../../ado/reference/ado-api/count-property-ado.md)属性。  
  
-   从集合中删除列[删除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映与当前数据库的架构集合中的对象[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
> [!NOTE]
>  追加时，将会出错**列**到**列**的集合[索引](../../../ado/reference/adox-api/index-object-adox.md)如果**列**中不存在[表](../../../ado/reference/adox-api/table-object-adox.md)已追加到[表](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
 本部分包含以下主题。  
  
-   [列集合属性、方法和事件](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [列和表 Append 方法、 Name 属性示例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [连接的 Close 方法、 表 Type 属性示例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [项 Append 方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 属性示例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [列对象 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
