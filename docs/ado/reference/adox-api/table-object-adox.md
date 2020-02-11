---
title: Table 对象（ADOX） |Microsoft Docs
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
ms.openlocfilehash: 10f3add3cb243d54643c3294104ec2546e7737d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965167"
---
# <a name="table-object-adox"></a>表对象 (ADOX)
表示包含列、索引和键的数据库表。  
  
## <a name="remarks"></a>备注  
 下面的代码创建一个新**表**：  
  
```  
Dim obj As New Table  
```  
  
 使用**Table**对象的属性和集合，可以：  
  
-   标识具有[Name 属性（ADOX）](../../../ado/reference/adox-api/name-property-adox.md)属性的表。  
  
-   确定具有[Type 属性（表）（ADOX）](../../../ado/reference/adox-api/type-property-table-adox.md)属性的表的类型。  
  
-   使用[columns 集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)集合访问表的数据库列。  
  
-   使用[索引集合（ADOX）](../../../ado/reference/adox-api/indexes-collection-adox.md)访问表的索引。  
  
-   使用[Keys 集合（ADOX）](../../../ado/reference/adox-api/keys-collection-adox.md)访问表的键。  
  
-   指定拥有具有[ParentCatalog 属性（ADOX）](../../../ado/reference/adox-api/parentcatalog-property-adox.md)属性的表的目录。  
  
-   返回具有[DateCreated 属性（adox）](../../../ado/reference/adox-api/datecreated-property-adox.md)和[DATEMODIFIED 属性（adox）](../../../ado/reference/adox-api/datemodified-property-adox.md)属性的日期信息。  
  
-   使用[Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)集合访问提供程序特定的表属性。  
  
> [!NOTE]
>  您的数据访问接口可能不支持**表**对象的所有属性。 如果为提供程序不支持的属性设置了值，则会发生错误。 对于新**表**对象，当对象追加到集合时，将发生错误。 对于现有对象，在设置属性时会发生此错误。  
>   
>  创建**表**对象时，是否存在可选属性的适当默认值并不保证提供程序支持该属性。 有关提供程序支持的属性的详细信息，请参阅提供程序文档。  
  
 本部分包含以下主题。  
  
-   [表对象属性、方法和事件](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录 ActiveConnection 属性示例（VB）](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [列和表追加方法，Name 属性示例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [连接关闭方法，表类型属性示例（VB）](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 属性示例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 属性示例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [列集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [索引集合（ADOX）](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [键集合（ADOX）](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
