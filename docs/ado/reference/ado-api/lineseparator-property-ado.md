---
title: LineSeparator 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b55f82e92ff74ba359074613205bc8086af81b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864451"
---
# <a name="lineseparator-property-ado"></a>LineSeparator 属性 (ADO)
指示要用作文本中的行分隔符的二进制字符[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)值，该值指示用中的行分隔符字符**Stream**。 默认值是**adCRLF**。  
  
## <a name="remarks"></a>备注  
 **LineSeparator**用于读取的文本内容时解释行**Stream**。 可以通过跳过行[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法。  
  
 **LineSeparator**仅用于文本**Stream**对象 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 如果忽略此属性**类型**是**adTypeBinary**。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
