---
description: AppendChunk 方法 (ADO)
title: " (ADO) 的 AppendChunk 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: rothja
ms.author: jroth
ms.openlocfilehash: 290155a3e6ea7e8ec0110d2bc2672cc74f6895b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451229"
---
# <a name="appendchunk-method-ado"></a>AppendChunk 方法 (ADO)
将数据追加到大文本或二进制数据 [字段](../../../ado/reference/ado-api/field-object.md)，或追加到 [参数](../../../ado/reference/ado-api/parameter-object.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>参数  
 对象  
 一个 **字段** 或 **参数** 对象。  
  
 *Data*  
 一个包含要追加到对象的数据的 **变量** 。  
  
## <a name="remarks"></a>备注  
 对**字段**或**参数**对象使用**AppendChunk**方法，以使用较长的二进制或字符数据填充它。 在系统内存有限的情况下，可以使用 **AppendChunk** 方法在部分中而不是完整地操作长值。  
  
## <a name="field"></a>字段  
 如果**字段**对象的[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)属性中的**adFldLong**位设置为**true**，则可以对该字段使用**AppendChunk**方法。  
  
 **Field**对象上的第一个**AppendChunk**调用将数据写入字段，并覆盖任何现有数据。 后续 **AppendChunk** 调用将添加到现有数据。 如果要将数据追加到一个字段，然后设置或读取当前记录中另一个字段的值，则 ADO 会假定您已完成将数据追加到第一个字段。 如果再次对第一个字段调用 **AppendChunk** 方法，则 ADO 会将调用解释为新的 **AppendChunk** 操作，并覆盖现有数据。 访问不是第一个**记录集**对象的克隆的其他[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象中的字段将不会中断**AppendChunk**操作。  
  
 如果对**字段**对象调用**AppendChunk**时没有当前记录，则会发生错误。  
  
> [!NOTE]
>  **AppendChunk**方法不[ (ADO) 对象在记录对象](../../../ado/reference/ado-api/record-object-ado.md)的**字段**对象上操作。 它不执行任何操作，并将生成运行时错误。  
  
## <a name="parameter"></a>参数  
 如果**参数**对象的**Attributes**属性中的**adParamLong**位设置为**true**，则可以对该参数使用**AppendChunk**方法。  
  
 **参数**对象上的第一个**AppendChunk**调用将数据写入参数，并覆盖任何现有数据。 后续 **AppendChunk** 对 **参数** 对象的调用将添加到现有参数数据。 传递 null 值的 **AppendChunk** 调用会丢弃所有参数数据。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [字段对象](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [参数对象](../../../ado/reference/ado-api/parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [AppendChunk 和 GetChunk 方法示例 (VB) ](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法示例 (VC + +) ](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [ADO)  (特性属性 ](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
