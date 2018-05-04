---
title: 编写方法 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77b4da5ba900cdd3456bbfe611ea0fe1021e23d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="write-method"></a>编写方法
写入二进制数据保存到[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parameters  
 *Buffer*  
 A **Variant** ，其中包含要写入的字节数组。  
  
## <a name="remarks"></a>注释  
 指定的字节写入到**流**不含任何干预空格每个字节之间的对象。  
  
 当前[位置](../../../ado/reference/ado-api/position-property-ado.md)设置为以下写入的数据的字节。 **编写**方法不截断流中的数据的其余部分。 如果要进行截断操作这些字节，调用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果您编写过去的当前[EOS](../../../ado/reference/ado-api/eos-property.md)位置，[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**流**将增加以包含任何新字节和**EOS**将移动至新的最后一字节在**流**。  
  
> [!NOTE]
>  **编写**方法用于二进制数据流 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeBinary**)。 文本流的 (**类型**是**adTypeText**)，使用[WriteText](../../../ado/reference/ado-api/writetext-method.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
