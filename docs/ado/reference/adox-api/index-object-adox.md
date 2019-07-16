---
title: 索引对象 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7bff462b7c9ffe115cdfd52d1ec1f0a810a50531
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966089"
---
# <a name="index-object-adox"></a>索引对象 (ADOX)
表示数据库表中的索引。  
  
## <a name="remarks"></a>备注  
 下面的代码创建一个新**索引**:  
  
```  
Dim obj As New Index  
```  
  
 使用属性和集合**索引**对象，你可以：  
  
-   标识与索引[名称](../../../ado/reference/adox-api/name-property-adox.md)属性。  
  
-   访问具有索引的数据库列[列](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
-   指定是否必须具有唯一索引键[Unique](../../../ado/reference/adox-api/unique-property-adox.md)属性。  
  
-   指定索引是否具有表的主键[PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md)属性。  
  
-   指定索引字段中具有 null 值的记录是否具有与索引条目[IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md)属性。  
  
-   指定是否使用聚集索引[Clustered](../../../ado/reference/adox-api/clustered-property-adox.md)属性。  
  
-   访问使用特定于访问接口的索引属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  追加时，将会出错[列](../../../ado/reference/adox-api/column-object-adox.md)到**列**的集合**索引**如果**列**中不存在[表](../../../ado/reference/adox-api/table-object-adox.md)已追加到的对象[表](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
> [!NOTE]
>  数据访问接口可能不支持的所有属性**索引**对象。 如果您设置的提供程序不支持的属性值，将会出错。 对新**索引**对象，该对象追加到集合时，将发生错误。 对于现有对象，将其设置属性时，将发生错误。  
  
> [!NOTE]
>  创建时**索引**对象，一个可选属性的相应默认值是否存在不保证您的提供程序支持该属性。 您的提供程序支持的属性有关的详细信息，请参阅提供程序文档。  
  
 本部分包含以下主题。  
  
-   [索引对象属性、方法和事件](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [索引 Append 方法示例 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [IndexNulls 属性示例 (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey 和 Unique 属性示例 (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder 属性示例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
