---
description: 索引对象 (ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 81f0bf8d07bbb89105a0ceab421d8433d52f1672
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439939"
---
# <a name="index-object-adox"></a>索引对象 (ADOX)
表示数据库表中的索引。  
  
## <a name="remarks"></a>备注  
 下面的代码创建一个新 **索引**：  
  
```  
Dim obj As New Index  
```  
  
 使用 **索引** 对象的属性和集合，可以：  
  
-   标识具有 [Name](../../../ado/reference/adox-api/name-property-adox.md) 属性的索引。  
  
-   使用 [columns](../../../ado/reference/adox-api/columns-collection-adox.md) 集合访问索引的数据库列。  
  
-   指定索引键是否必须具有[唯一属性。](../../../ado/reference/adox-api/unique-property-adox.md)  
  
-   指定索引是否为具有 [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) 属性的表的主键。  
  
-   指定在其索引字段中具有 null 值的记录是否具有具有 [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) 属性的索引条目。  
  
-   指定是否用 [聚集](../../../ado/reference/adox-api/clustered-property-adox.md) 属性对索引进行聚集。  
  
-   使用 [properties](../../../ado/reference/ado-api/properties-collection-ado.md) 集合访问提供程序特定的索引属性。  
  
> [!NOTE]
>  如果表中已追加到[Tables](../../../ado/reference/adox-api/tables-collection-adox.md)集合的[表](../../../ado/reference/adox-api/table-object-adox.md)对象中不**存在列，** 则将[该列](../../../ado/reference/adox-api/column-object-adox.md)追加到**索引**的**Columns**集合中时，将出现错误。  
  
> [!NOTE]
>  数据访问接口可能不支持 **Index** 对象的所有属性。 如果为该访问接口不支持的属性设置值，则会出现错误。 对于新 **索引** 对象，当对象追加到集合时，将发生错误。 对于现有对象，在设置属性时会发生此错误。  
  
> [!NOTE]
>  创建 **索引** 对象时，是否存在可选属性的适当默认值并不保证提供程序支持该属性。 有关提供程序支持的属性的详细信息，请参阅提供程序文档。  
  
 本部分包含以下主题。  
  
-   [索引对象属性、方法和事件](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [ (VB 的索引 Append 方法示例) ](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [IndexNulls 属性示例 (VB) ](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey 和 Unique 属性示例 (VB) ](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder 属性示例 (VB) ](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [列集合 (ADOX) ](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [索引集合 (ADOX) ](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
