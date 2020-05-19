---
title: Append 方法（ADOX 索引） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: rothja
ms.author: jroth
ms.openlocfilehash: 6996f3a0a3ad9f2ffa727a6cbd7b48d3fbf32777
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764058"
---
# <a name="append-method-adox-indexes"></a>Append 方法（ADOX 索引）
将新[索引](../../../ado/reference/adox-api/index-object-adox.md)对象添加到[索引](../../../ado/reference/adox-api/indexes-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>参数  
 *索引*  
 要追加的**索引**对象或要创建并追加的索引的名称。  
  
 *“列”*  
 可选。 一个**变量**值，指定要编制索引的列的名称。 *Columns*参数对应于[列](../../../ado/reference/adox-api/column-object-adox.md)对象或对象的[Name](../../../ado/reference/adox-api/name-property-adox.md)属性的值。  
  
## <a name="remarks"></a>备注  
 *Columns*参数可以采用列的名称或列名的数组。  
  
 如果提供程序不支持创建索引，则会出现错误。  
  
## <a name="applies-to"></a>应用于  
 [索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [索引 Append 方法示例（VB）](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append 方法（ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
