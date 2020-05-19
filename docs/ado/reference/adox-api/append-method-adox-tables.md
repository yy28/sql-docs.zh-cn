---
title: Append 方法（ADOX 表） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 19617c65b350527753895ed613f671c3ac0f88e8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764008"
---
# <a name="append-method-adox-tables"></a>Append 方法（ADOX 表）
向[Tables](../../../ado/reference/adox-api/tables-collection-adox.md)集合添加一个新的[Table](../../../ado/reference/adox-api/table-object-adox.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>参数  
 *表*  
 一个包含对要追加的**表**的引用的**变量**值，或者是要创建并追加的表的名称。  
  
## <a name="remarks"></a>备注  
 如果提供程序不支持创建表，则会发生错误。  
  
## <a name="applies-to"></a>应用于  
 [表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [列和表追加方法，Name 属性示例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [ParentCatalog 属性示例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append 方法（ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
