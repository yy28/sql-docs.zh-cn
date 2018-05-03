---
title: LineSeparator 属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f46f6cdf8b3c8fccf9da41818aaeb2fb63fefbe6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lineseparator-property-ado"></a>LineSeparator 属性 (ADO)
指示要用作文本中的行分隔符的二进制字符[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)值，该值指示在中使用的行分隔符字符**流**。 默认值是**adCRLF**。  
  
## <a name="remarks"></a>注释  
 **LineSeparator**用于解释行，读取的文本内容时**流**。 可以使用跳过行[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法。  
  
 **LineSeparator**仅用于文本**流**对象 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 如果忽略此属性**类型**是**adTypeBinary**。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
