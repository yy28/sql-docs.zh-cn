---
title: 列对象 (ADOX) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d8c2fc9ff3732e3d8330813a16f3605b2fd3c03
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="column-object-adox"></a>列对象 (ADOX)
从表、 索引或键表示的列。  
  
## <a name="remarks"></a>注释  
 下面的代码创建一个新**列**:  
  
 `Dim obj As New Column`  
  
 使用属性和集合**列**对象，你可以：  
  
-   标识与列[名称属性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)属性。  
  
-   指定的列的数据类型[类型属性 （密钥） (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)属性。  
  
-   确定如果列为固定长度或它可以包含空值与[特性属性 (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md)属性。  
  
-   指定的列的最大大小[DefinedSize 属性 (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md)属性。  
  
-   对于数字数据值，指定与刻度[NumericScale 属性 (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md)属性。  
  
-   对于数值数据值，指定与的最大精度[精度属性 (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)属性。  
  
-   指定[目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)拥有的列[ParentCatalog 属性 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md)属性。  
  
-   对于键列，相关表中指定相关列的名称[RelatedColumn 属性 (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)属性。  
  
-   对于索引列指定排序顺序是升序还是降序与[SortOrder 属性 (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md)属性。  
  
-   访问与提供程序特定属性[属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  并非所有属性的**列**数据提供程序可能支持对象。 如果设置了该提供程序不支持属性的值，将会出错。 新**列**对象，该对象追加到集合时，将发生此错误。 对于现有对象，将其设置属性时，将发生错误。  
>   
>  在创建时**列**对象，一个可选属性的相应默认值是否存在不保证你的提供商支持该属性。 你的提供商支持的属性有关的详细信息，请参阅提供程序文档。  
  
 本部分包含以下主题。  
  
-   [列对象属性、方法和事件](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [列和表追加方法名称的属性示例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [连接关闭方法，表类型的属性示例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [密钥追加方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX 代码示例： NumericScale 和精度属性示例 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 属性示例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
