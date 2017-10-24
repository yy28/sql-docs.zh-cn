---
title: "Append 方法 （ADOX 索引） |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb25d4ce8ab95f1311460f67b79a2b2199b96e62
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-indexes"></a>Append 方法 （ADOX 索引）
添加新[索引](../../../ado/reference/adox-api/index-object-adox.md)对象传递给[索引](../../../ado/reference/adox-api/indexes-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parameters  
 *索引*  
 **索引**要追加的对象或要创建并追加的索引的名称。  
  
 *列*  
 可选。 A **Variant**值，该值指定要编制索引的列的名称。 *列*参数对应的值[名称](../../../ado/reference/adox-api/name-property-adox.md)属性[列](../../../ado/reference/adox-api/column-object-adox.md)对象。  
  
## <a name="remarks"></a>注释  
 *列*参数可以采用的列名称或列名称的数组。  
  
 如果提供程序不支持创建索引，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [索引追加方法示例 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 （ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)

