---
title: 表对象 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 43679897bf49e9a2505dad1540f3b494b66f180d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705860"
---
# <a name="table-object-adox"></a>表对象 (ADOX)
表示包括列、 索引和键的数据库表。  
  
## <a name="remarks"></a>备注  
 下面的代码创建一个新**表**:  
  
```  
Dim obj As New Table  
```  
  
 使用属性和集合**表**对象，你可以：  
  
-   标识与该表[名称属性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)属性。  
  
-   确定具有表的类型[类型属性 （表） (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)属性。  
  
-   访问包含表的数据库列[列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
-   访问具有表的索引[索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)。  
  
-   访问具有表的密钥[密钥集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)。  
  
-   指定拥有具有目录[ParentCatalog 属性 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md)属性。  
  
-   返回日期信息与[DateCreated 属性 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)并[DateModified 属性 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)属性。  
  
-   访问使用特定于提供程序的表属性[属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  数据访问接口可能不支持的所有属性**表**对象。 如果您设置的提供程序不支持的属性值，将会出错。 对新**表**对象，该对象追加到集合时，将发生错误。 对于现有对象，将其设置属性时，将发生错误。  
>   
>  创建时**表**对象，一个可选属性的相应默认值是否存在不保证您的提供程序支持该属性。 您的提供程序支持的属性有关的详细信息，请参阅提供程序文档。  
  
 本部分包含以下主题。  
  
-   [表对象属性、方法和事件](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [目录 ActiveConnection 属性示例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [列和表 Append 方法、 Name 属性示例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [连接的 Close 方法、 表 Type 属性示例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [项 Append 方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [项集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
