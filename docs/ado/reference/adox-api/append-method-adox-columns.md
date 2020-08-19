---
description: Append 方法（ADOX 列）
title: ) 的 ADOX 列 (追加方法 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bd33dc71c9adcbe8e6ed25f965b227fbc76d96fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440519"
---
# <a name="append-method-adox-columns"></a>Append 方法（ADOX 列）
向[Columns](../../../ado/reference/adox-api/columns-collection-adox.md)集合添加一个新的[列](../../../ado/reference/adox-api/column-object-adox.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>参数  
 *列*  
 要追加的 **列** 对象或者要创建并追加的列的名称。  
  
 *类型*  
 可选。 指定列的数据类型的 **Long** 值。 *类型*参数对应于**列**对象的[type](../../../ado/reference/adox-api/type-property-column-adox.md)属性。  
  
 *DefinedSize*  
 可选。 指定列的大小的 **Long** 值。 *DefinedSize*参数对应于**列**对象的[DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md)属性。  
  
> [!NOTE]
>  如果**列**不存在于已追加到[Tables](../../../ado/reference/adox-api/tables-collection-adox.md)集合的[表](../../../ado/reference/adox-api/table-object-adox.md)中，则当向[索引](../../../ado/reference/adox-api/index-object-adox.md)的**Columns**集合追加**列**时，将发生错误。  
  
## <a name="applies-to"></a>适用于  
 [列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [列和表追加方法、Name 属性示例 (VB) ](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule Properties Example (VB) ](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 属性示例 (VB) ](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [将方法追加 (ADOX 组) ](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 索引 (Append 方法) ](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [追加方法 (ADOX 密钥) ](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [附加方法 (ADOX 过程) ](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 表 (追加方法) ](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [ADOX 用户 (追加方法) ](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
