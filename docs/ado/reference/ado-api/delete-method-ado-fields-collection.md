---
description: Delete 方法（ADO 字段集合）
title: " (ADO 字段集合) 的删除方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 11499e3483af13ce5fc9edea8fd69694d36be9c7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974128"
---
# <a name="delete-method-ado-fields-collection"></a>Delete 方法（ADO 字段集合）
从 " [字段](../../../ado/reference/ado-api/fields-collection-ado.md) " 集合中删除一个对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>参数  
 *字段*  
 指定要删除的[字段](../../../ado/reference/ado-api/field-object.md)对象的**变量**。 此参数可以是 **字段** 对象的名称，也可以是 **字段** 对象本身的序号位置。  
  
## <a name="remarks"></a>注解  
 对打开的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)调用**Delete**方法会导致运行时错误。  
  
## <a name="applies-to"></a>适用于  
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ (ADO 参数集合的 Delete 方法) ](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [ADO 记录集 (Delete 方法) ](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
