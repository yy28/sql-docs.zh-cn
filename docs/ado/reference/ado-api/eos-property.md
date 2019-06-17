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
manager: jroth
ms.openlocfilehash: 10b7ee78cb9903ccf0794a197a0679c226141641
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698256"
---
# <a name="eos-property"></a>EOS 属性
指示当前位置是否在末尾[流](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="return-values"></a>返回值  
 返回**布尔**值，该值指示当前的位置是否位于流结尾。 **EOS**将返回**True**如果有没有更多字节流，则它将返回**False**如果有多个字节遵循当前的位置。  
  
 若要设置流的位置结束，使用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。 若要确定当前的位置，请使用[位置](../../../ado/reference/ado-api/position-property-ado.md)属性。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [EOS 和 LineSeparator 属性 SkipLine 方法示例 (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
