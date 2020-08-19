---
description: ActualSize 属性 (ADO)
title: " (ADO) 的 ActualSize 属性 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 53384838d53003f0c4f81ec3b629e987ce2649a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451629"
---
# <a name="actualsize-property-ado"></a>ActualSize 属性 (ADO)
指示字段值的实际长度（以字节为单位）。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 返回一个 **长整型** 值。  
  
## <a name="remarks"></a>备注  
 使用 **ActualSize** 属性可以返回 [字段](../../../ado/reference/ado-api/field-object.md) 对象的值的实际长度。 对于所有字段， **ActualSize** 属性是只读的。 如果 ADO 无法确定 **字段** 对象的值的长度，则 **ActualSize** 属性将返回 **adUnknown**。  
  
 **ActualSize**和[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)属性不同，如以下示例中所示。 声明类型为**adVarChar**且最大长度为50个字符的**Field**对象将返回**DefinedSize**属性值50，但它返回的**ActualSize**属性值是存储在当前记录的字段中的数据的长度。 **DefinedSize**大于255字节的**字段**将被视为可变长度列。  
  
## <a name="applies-to"></a>适用于  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActualSize 和 DefinedSize 属性示例 (VB) ](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 属性示例 (VC + +) ](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 属性](../../../ado/reference/ado-api/definedsize-property.md)
