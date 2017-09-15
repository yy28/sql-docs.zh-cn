---
title: "ActualSize 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d66019d7a71dd480f1a88a28fe94d72a176497c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="actualsize-property-ado"></a>ActualSize 属性 (ADO)
指示字段的实际长度???s 以字节为单位的值。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 返回**长**值。  
  
## <a name="remarks"></a>注释  
 使用**ActualSize**属性返回的实际长度[字段](../../../ado/reference/ado-api/field-object.md)对象的值。 为所有字段， **ActualSize**属性是只读的。 如果 ADO 无法确定的长度**字段**对象的值， **ActualSize**属性返回**adUnknown**。  
  
 **ActualSize**和[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)属性发生变化，如下面的示例中所示。 A**字段**的声明的类型的对象**以便您可以排除**和 50 个字符的最大长度返回**DefinedSize**属性值为 50，但**ActualSize**它将返回的属性值是当前记录的字段中存储的数据的长度。 **字段**与**DefinedSize**大于 255 个字节将被视为可变长度列。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActualSize 和 DefinedSize 属性示例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 属性示例 （VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 属性](../../../ado/reference/ado-api/definedsize-property.md)

