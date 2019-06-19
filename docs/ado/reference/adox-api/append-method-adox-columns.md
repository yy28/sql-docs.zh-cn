---
title: Append 方法 （ADOX 列） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e8ac03231680ecd807234b20ac7b210bc480f2c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708484"
---
# <a name="append-method-adox-columns"></a>Append 方法（ADOX 列）
添加一个新[列](../../../ado/reference/adox-api/column-object-adox.md)对象传递给[列](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parameters  
 *列*  
 **列**对象以追加或要创建并追加的列的名称。  
  
 *类型*  
 可选。 一个**长**值，该值指定列的数据类型。 *类型*参数对应于[类型](../../../ado/reference/adox-api/type-property-column-adox.md)属性**列**对象。  
  
 *DefinedSize*  
 可选。 一个**长**值，该值指定列的大小。 *DefinedSize*参数对应于[DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md)属性**列**对象。  
  
> [!NOTE]
>  追加时，将会出错**列**到**列**的集合[索引](../../../ado/reference/adox-api/index-object-adox.md)如果**列**中不存在[表](../../../ado/reference/adox-api/table-object-adox.md)已追加到[表](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
## <a name="applies-to"></a>适用范围  
 [列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [列和表 Append 方法、 Name 属性示例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [项 Append 方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 项）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
