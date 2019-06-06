---
title: Clear 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d35df7a036f41d74ce0a3fc94c3adef1abae91c3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718509"
---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
移除所有[错误](../../../ado/reference/ado-api/error-object.md)中的对象[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>备注  
 使用**清晰**方法[错误](../../../ado/reference/ado-api/errors-collection-ado.md)要从中删除所有现有集合[错误](../../../ado/reference/ado-api/error-object.md)集合中的对象。 出现错误时，会自动清除 ADO**错误**集合，并填充其与**错误**对象根据新的错误。  
  
 某些属性和方法返回显示为警告**错误**中的对象**错误**集合但不是会停止程序执行。 在调用之前[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)上的方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象;[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象; 或者设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性**记录集**对象，请调用**清除**上的方法**错误**集合。 这样一来，可以读取[计数](../../../ado/reference/ado-api/count-property-ado.md)的属性**错误**集合以测试是否返回警告。  
  
## <a name="applies-to"></a>适用范围  
 [错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [执行、 再次查询和清除方法示例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [执行、 再次查询和清除方法示例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、 再次查询和清除方法示例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 方法 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [筛选器属性](../../../ado/reference/ado-api/filter-property.md)   
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
