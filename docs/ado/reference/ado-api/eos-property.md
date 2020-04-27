---
title: EOS 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a19856c957ee0c003e934ff8b2632aa28e32d33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918918"
---
# <a name="eos-property"></a>EOS 属性
指示当前位置是否在[流](../../../ado/reference/ado-api/stream-object-ado.md)的末尾。  
  
## <a name="return-values"></a>返回值  
 返回一个**布尔**值，该值指示当前位置是否在流的末尾。 如果流中没有更多字节，则**EOS**返回**True** ;如果当前位置后面有更多字节，则返回**False** 。  
  
 若要设置流位置的结束位置，请使用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。 若要确定当前位置，请使用[position](../../../ado/reference/ado-api/position-property-ado.md)属性。  
  
## <a name="applies-to"></a>应用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [EOS 和 LineSeparator 属性和 SkipLine 方法示例（VB）](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
