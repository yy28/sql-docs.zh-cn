---
title: Delete 方法 （ADO 字段集合） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9db49905b6548e5cb21cca976683c8b387017d32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919134"
---
# <a name="delete-method-ado-fields-collection"></a>Delete 方法（ADO 字段集合）
删除从对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parameters  
 *字段*  
 一个**Variant** ，它指定留存[字段](../../../ado/reference/ado-api/field-object.md)要删除对象。 此参数可以是名称**字段**对象或的序号位置**字段**对象本身。  
  
## <a name="remarks"></a>备注  
 调用**Fields.Delete**处于打开状态的方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)会导致运行时错误。  
  
## <a name="applies-to"></a>适用范围  
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Delete 方法 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
