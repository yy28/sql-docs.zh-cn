---
title: OriginalValue 属性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d25c44883c7f04f1543639ecc870c00ad5beb9d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240006"
---
# <a name="originalvalue-property-ado"></a>OriginalValue 属性 (ADO)
指示的值[字段](../../../ado/reference/ado-api/field-object.md)进行任何更改之前存在该记录。  
  
## <a name="return-value"></a>返回值  
 返回**变体**值，该值表示在任何更改前的字段的值。  
  
## <a name="remarks"></a>备注  
 使用**OriginalValue**属性以返回从当前记录的字段的原始字段值。  
  
 在中*立即更新模式*(在其中提供程序将更改写入到基础数据源调用后[更新](../../../ado/reference/ado-api/update-method.md)方法)，则**OriginalValue**属性将返回任何更改之前存在的字段值 (即，自上次**更新**方法调用)。 这是相同的值，该值[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法使用替换[值](../../../ado/reference/ado-api/value-property-ado.md)属性。  
  
 在中*批更新模式*(提供程序将多个更改缓存并将其写入到基础数据源仅在调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法)，则**OriginalValue**属性返回的任何更改之前存在的字段值 (即，自上次**UpdateBatch**方法调用)。 这是相同的值，该值[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法使用替换**值**属性。 当使用此属性与[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)属性，可以解析从批处理更新而引起的冲突。  
  
## <a name="record"></a>录制  
 有关[记录](../../../ado/reference/ado-api/record-object-ado.md)对象， **OriginalValue**属性将为空的字段前添加[更新](../../../ado/reference/ado-api/update-method.md)调用。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>请参阅  
 [OriginalValue 和 UnderlyingValue 属性示例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 属性示例 （VC + +）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 属性](../../../ado/reference/ado-api/underlyingvalue-property.md)
