---
title: Append 方法 （ADOX 表） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Tables::Append
- Tables::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: a362ed51-314c-4783-9598-538dbf755f3d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 75a5405ef51ea8bfe2d365796b311cbaa36b2d0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708366"
---
# <a name="append-method-adox-tables"></a>Append 方法（ADOX 表）
添加一个新[表](../../../ado/reference/adox-api/table-object-adox.md)对象传递给[表](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>Parameters  
 *表*  
 一个**Variant**值，该值包含对引用**表**追加或要创建并追加的表的名称。  
  
## <a name="remarks"></a>备注  
 如果提供程序不支持创建表，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [列和表 Append 方法、 Name 属性示例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 项）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
