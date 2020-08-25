---
description: Clear 方法 (ADO)
title: " (ADO) 的 Clear 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b7ed940248230d1c7b74f6782abcb555a538021
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776266"
---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
从[错误](./errors-collection-ado.md)集合中移除所有[错误](./error-object.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>备注  
 对[Errors](./errors-collection-ado.md)集合使用**Clear**方法可从集合中删除所有现有的[错误](./error-object.md)对象。 出现错误时，ADO 会自动清除 **错误** 集合，并根据新错误将 **错误** 对象填充到其中。  
  
 某些属性和方法会返回**错误**集合中显示为**错误**对象的警告，但不会停止执行程序。 在对[Recordset](./recordset-object-ado.md)对象调用[Resync](./resync-method.md)、 [UpdateBatch](./updatebatch-method.md)或[CancelBatch](./cancelbatch-method-ado.md)方法之前，[连接](./connection-object-ado.md)对象上的[Open](./open-method-ado-connection.md)方法;或在**记录集**对象上设置[Filter](./filter-property.md)属性，对**Errors**集合调用**Clear**方法。 通过这种方式，您可以读取**Errors**集合的[Count](./count-property-ado.md)属性来测试返回的警告。  
  
## <a name="applies-to"></a>适用于  
 [错误集合 (ADO)](./errors-collection-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [执行、再次查询和清除方法示例 (VB) ](./execute-requery-and-clear-methods-example-vb.md)   
 [ (VBScript) 执行、再次查询和清除方法示例 ](./execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、再次查询和清除方法示例 (VC + +) ](./execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 方法 (ADO) ](./cancelbatch-method-ado.md)   
 [ (ADO 字段集合的 Delete 方法) ](./delete-method-ado-fields-collection.md)   
 [ (ADO 参数集合的 Delete 方法) ](./delete-method-ado-parameters-collection.md)   
 [ADO 记录集 (Delete 方法) ](./delete-method-ado-recordset.md)   
 [筛选器属性](./filter-property.md)   
 [重新同步方法](./resync-method.md)   
 [UpdateBatch 方法](./updatebatch-method.md)