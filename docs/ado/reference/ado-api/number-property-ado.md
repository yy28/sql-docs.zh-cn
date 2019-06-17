---
title: Number 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4ef1665bf96688fba5fc7d157b73d2df2fcd2c68
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705609"
---
# <a name="number-property-ado"></a>Number 属性 (ADO)
指示唯一标识的数字[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**长**可能与之一相对应的值[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)常量。  
  
## <a name="remarks"></a>备注  
 使用**数**属性来确定发生的错误。 属性的值是对应于错误条件的唯一编号。  
  
 [错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合返回一个 HRESULT，以十六进制格式 (例如，0x80004005) 或长整型值 (例如，2147467259)。 可以由基础组件，如 OLE DB 或甚至 OLE 本身引发这些 Hresult。 有关这些数字的详细信息，请参阅[错误 (OLE DB)](https://msdn.microsoft.com/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd)中[OLE DB 程序员参考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) *。*  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>请参阅  
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 属性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext、 HelpFile 属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Source 属性（ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)
