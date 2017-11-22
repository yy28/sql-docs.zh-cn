---
title: "Delete 方法 （ADO 参数集合） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords: Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b58c32020f5a73f293fe0bd679e253e3bcad0ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="delete-method-ado-parameters-collection"></a>Delete 方法 （ADO 参数集合）
删除从对象[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parameters  
 *Index*  
 A**字符串**值，该值在集合中包含你想要删除的对象或对象的序号位置 （索引） 的名称。  
  
## <a name="remarks"></a>注释  
 使用**删除**集合上的方法使你可以删除集合中的其中一个对象。 此方法是仅适用于**参数**集合[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。 必须使用[参数](../../../ado/reference/ado-api/parameter-object.md)对象的[名称](../../../ado/reference/ado-api/name-property-ado.md)属性或调用时其集合索引**删除**方法-对象变量不是有效的参数。  
  
## <a name="applies-to"></a>适用范围  
 [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Delete 方法 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
