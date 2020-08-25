---
description: LineSeparator 属性 (ADO)
title: " (ADO) 的 LineSeparator 属性 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fe0976fda4a390f93f7d634fac9e1cbc52104b29
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774626"
---
# <a name="lineseparator-property-ado"></a>LineSeparator 属性 (ADO)
指示要在文本 [流](./stream-object-ado.md) 对象中用作行分隔符的二进制字符。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 [LineSeparatorsEnum](./lineseparatorsenum.md) 值，该值指示 **流**中使用的行分隔符。 默认值为 **adCRLF**。  
  
## <a name="remarks"></a>备注  
 **LineSeparator** 用于在读取文本 **流**内容时解释行。 可以通过 [SkipLine](./skipline-method.md) 方法跳过行。  
  
 **LineSeparator**仅与 ([类型](./type-property-ado-stream.md)为**adTypeText**) 的文本**流**对象一起使用。 如果 **类型** 是 **adTypeBinary**，则忽略此属性。  
  
## <a name="applies-to"></a>适用于  
 [流对象 (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [流对象 (ADO)](./stream-object-ado.md)