---
title: Delete 方法 （ADO 字段集合） |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 296364d3fafc4a67767699d55631209658657de1
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277546"
---
# <a name="delete-method-ado-fields-collection"></a>Delete 方法 （ADO 字段集合）
删除从对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parameters  
 *字段*  
 A **Variant**可为指定[字段](../../../ado/reference/ado-api/field-object.md)要删除对象。 此参数可以为的名称**字段**对象或的序号位置**字段**对象本身。  
  
## <a name="remarks"></a>Remarks  
 调用**Fields.Delete**处于打开状态的方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)将导致运行时错误。  
  
## <a name="applies-to"></a>适用范围  
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Delete 方法 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
