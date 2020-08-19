---
description: Delete 方法（ADO 字段集合）
title: " (ADO 字段集合) 的删除方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
author: rothja
ms.author: jroth
ms.openlocfilehash: fb60cea6ef2e741103e94f38955bb2afc688e228
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444169"
---
# <a name="delete-method-ado-fields-collection"></a>Delete 方法（ADO 字段集合）
从 " [字段](../../../ado/reference/ado-api/fields-collection-ado.md) " 集合中删除一个对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>参数  
 字段  
 指定要删除的[字段](../../../ado/reference/ado-api/field-object.md)对象的**变量**。 此参数可以是 **字段** 对象的名称，也可以是 **字段** 对象本身的序号位置。  
  
## <a name="remarks"></a>备注  
 对打开的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)调用**Delete**方法会导致运行时错误。  
  
## <a name="applies-to"></a>适用于  
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ (ADO 参数集合的 Delete 方法) ](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [ADO 记录集 (Delete 方法) ](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
