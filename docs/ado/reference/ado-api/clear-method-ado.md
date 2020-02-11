---
title: Clear 方法（ADO） |Microsoft Docs
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
ms.openlocfilehash: 96bd13f130966b1830d07e49633842e4154b52b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920067"
---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
从[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合中移除所有[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>备注  
 对[Errors](../../../ado/reference/ado-api/errors-collection-ado.md)集合使用**Clear**方法可从集合中删除所有现有的[错误](../../../ado/reference/ado-api/error-object.md)对象。 出现错误时，ADO 会自动清除**错误**集合，并根据新错误将**错误**对象填充到其中。  
  
 某些属性和方法会返回**错误**集合中显示为**错误**对象的警告，但不会停止执行程序。 在对[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象调用[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法之前，[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象上的[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法;或在**记录集**对象上设置[Filter](../../../ado/reference/ado-api/filter-property.md)属性，对**Errors**集合调用**Clear**方法。 通过这种方式，您可以读取**Errors**集合的[Count](../../../ado/reference/ado-api/count-property-ado.md)属性来测试返回的警告。  
  
## <a name="applies-to"></a>应用于  
 [错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [执行、再次查询和清除方法示例（VB）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [执行、再次查询和清除方法示例（VBScript）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、再次查询和清除方法示例（VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 方法（ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法（ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法（ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [筛选器属性](../../../ado/reference/ado-api/filter-property.md)   
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
