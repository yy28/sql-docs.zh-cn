---
title: "Clear 方法 (ADO) |Microsoft 文档"
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
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 831ec9b295ca4e3d81707cfc2c1cc14169d1527c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
中删除所有[错误](../../../ado/reference/ado-api/error-object.md)对象从[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>注释  
 使用**清除**方法[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合中移除所有现有[错误](../../../ado/reference/ado-api/error-object.md)从集合的对象。 发生错误时，自动清除 ADO**错误**集合和填充其与**错误**对象基于新的错误。  
  
 某些属性和方法返回显示为警告**错误**中的对象**错误**集合但不是会停止对程序的执行。 在调用之前[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象;[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象; 或设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性**记录集**对象，请调用**清除**方法**错误**集合。 这样一来，你可以阅读[计数](../../../ado/reference/ado-api/count-property-ado.md)属性**错误**集合以测试是否返回警告。  
  
## <a name="applies-to"></a>适用范围  
 [错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [执行、 重新执行查询，并清除方法示例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [执行、 重新执行查询，并清除方法示例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、 重新执行查询，并清除方法示例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [执行方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 方法 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [筛选器属性](../../../ado/reference/ado-api/filter-property.md)   
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)

