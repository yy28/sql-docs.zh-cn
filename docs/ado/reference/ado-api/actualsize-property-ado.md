---
title: ActualSize 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d405113044d10244d8c4fc3483c6220bf630dc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921421"
---
# <a name="actualsize-property-ado"></a>ActualSize 属性 (ADO)
指示字段的值以字节为单位的实际长度。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 返回**长**值。  
  
## <a name="remarks"></a>备注  
 使用**ActualSize**属性返回的实际长度[字段](../../../ado/reference/ado-api/field-object.md)对象的值。 为所有字段**ActualSize**属性是只读的。 如果 ADO 无法确定的长度**字段**对象的值**ActualSize**属性返回**adUnknown**。  
  
 **ActualSize**并[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)属性有所不同，如下面的示例中所示。 一个**字段**对象的声明的类型**adVarChar** ，并返回最大长度 50 个字符**DefinedSize**属性值为 50，但**ActualSize**它将返回的属性值是当前记录的字段中存储的数据的长度。 **字段**与**DefinedSize**大于 255 个字节将被视为可变长度列。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>请参阅  
 [ActualSize 和 DefinedSize 属性示例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 属性示例 （VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 属性](../../../ado/reference/ado-api/definedsize-property.md)
