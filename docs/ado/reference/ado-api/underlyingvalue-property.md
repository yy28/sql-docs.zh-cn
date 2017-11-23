---
title: "UnderlyingValue 属性 |Microsoft 文档"
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
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords: UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d4f3014350f4e29461a6208802d3f82f8c95535
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 属性
指示的当前值[字段](../../../ado/reference/ado-api/field-object.md)数据库中的对象。  
  
## <a name="return-value"></a>返回值  
 返回**Variant**值，该值指示的值**字段**。  
  
## <a name="remarks"></a>注释  
 使用**UnderlyingValue**属性以从数据库中返回当前的字段值。 中的字段值**UnderlyingValue**属性是对你的交易可见，则可能会由另一个事务的新更新的结果的值。 这可能不同于[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)属性，反映了已向最初返回的值[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 这是类似于使用[重新同步](../../../ado/reference/ado-api/resync-method.md)方法，但**UnderlyingValue**属性从当前记录返回仅特定字段的值。 这是相同的值，[重新同步](../../../ado/reference/ado-api/resync-method.md)方法使用取代[值](../../../ado/reference/ado-api/value-property-ado.md)属性。  
  
 当你使用此属性与**OriginalValue**属性，您可以解决冲突所带来的批处理更新。  
  
## <a name="record"></a>录制  
 有关[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，此属性将为空的字段之前添加[更新](../../../ado/reference/ado-api/update-method.md)调用。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [OriginalValue 和 UnderlyingValue 属性示例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 属性示例 （VC + +）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue 属性 (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)
