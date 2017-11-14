---
title: "OriginalValue 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 018f07a06e96f9284d0a8e63742a5abebca925e1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="originalvalue-property-ado"></a>OriginalValue 属性 (ADO)
指示的值[字段](../../../ado/reference/ado-api/field-object.md)进行任何更改之前存在的记录。  
  
## <a name="return-value"></a>返回值  
 返回**Variant**值，该值表示任何更改之前字段的值。  
  
## <a name="remarks"></a>注释  
 使用**OriginalValue**属性从当前记录返回的字段的原始字段值。  
  
 在*立即更新模式*(在其中提供程序将更改写入基础数据源后调用[更新](../../../ado/reference/ado-api/update-method.md)方法)，则**OriginalValue**属性将返回任何更改之前存在的字段值 (即，自上次操作后**更新**方法调用)。 这是相同的值，[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法使用取代[值](../../../ado/reference/ado-api/value-property-ado.md)属性。  
  
 在*批处理更新模式下*(在其中提供程序缓存多个更改，并将其写入到基础数据源仅在调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法)，则**OriginalValue**属性返回的任何更改之前存在的字段值 (即，自上次操作后**UpdateBatch**方法调用)。 这是相同的值，[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法使用取代**值**属性。 当你使用此属性与[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)属性，您可以解决冲突所带来的批处理更新。  
  
## <a name="record"></a>录制  
 有关[记录](../../../ado/reference/ado-api/record-object-ado.md)对象， **OriginalValue**属性将为空的字段之前添加[更新](../../../ado/reference/ado-api/update-method.md)调用。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [OriginalValue 和 UnderlyingValue 属性示例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 属性示例 （VC + +）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 属性](../../../ado/reference/ado-api/underlyingvalue-property.md)

