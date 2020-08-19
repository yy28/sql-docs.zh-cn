---
description: OriginalValue 属性 (ADO)
title: " (ADO) 的 OriginalValue 属性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
author: rothja
ms.author: jroth
ms.openlocfilehash: 13353013575db87f5ec30ceb8cf4a5aab6a06079
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443119"
---
# <a name="originalvalue-property-ado"></a>OriginalValue 属性 (ADO)
指示在进行任何更改之前，记录中是否存在 [字段](../../../ado/reference/ado-api/field-object.md) 的值。  
  
## <a name="return-value"></a>返回值  
 返回一个表示字段值的 **变量** 值，此值在任何更改之前。  
  
## <a name="remarks"></a>备注  
 使用 **OriginalValue** 属性可以返回当前记录中字段的原始字段值。  
  
 在 *即时更新模式下* (在调用 [update](../../../ado/reference/ado-api/update-method.md) 方法) 后，提供程序将更改写入基础数据源， **OriginalValue** 属性返回在任何更改前存在的字段值 (也就是说，自上次 **更新** 方法调用) 之后。 此值与 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 方法用来替换 [value](../../../ado/reference/ado-api/value-property-ado.md) 属性的值相同。  
  
 在 *批处理更新模式下* (提供程序将在其中缓存多个更改，并仅在调用 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 方法) 时将这些更改写入基础数据源，而 **OriginalValue** 属性返回在任何更改前存在的字段值 (也就是说，自上次 **UpdateBatch** 方法调用) 。 此值与 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 方法用来替换 **value** 属性的值相同。 当你将此属性与 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) 属性一起使用时，你可以解决因批更新引起的冲突。  
  
## <a name="record"></a>Record  
 对于[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，在调用[Update](../../../ado/reference/ado-api/update-method.md)之前添加的字段的**OriginalValue**属性将为空。  
  
## <a name="applies-to"></a>适用于  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [OriginalValue 和 UnderlyingValue 属性示例 (VB) ](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 属性示例 (VC + +) ](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 属性](../../../ado/reference/ado-api/underlyingvalue-property.md)
