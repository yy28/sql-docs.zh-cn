---
description: SetEOS 方法
title: SetEOS 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ffe6f7d4a8861fb58f3b72f2b75de3de1ac9736
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777486"
---
# <a name="seteos-method"></a>SetEOS 方法
设置流的结束位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>备注  
 **SetEOS**通过[使当前位置成为流末尾，来](./position-property-ado.md)更新[EOS](./eos-property.md)属性的值。 位于当前位置后面的任何字节或字符都将被截断。  
  
 由于 [Write](./write-method.md)、 [WriteText](./writetext-method.md)和 [CopyTo](./copyto-method-ado.md) 不会截断现有 **流** 对象中的任何额外值，因此可以通过使用 **SetEOS**设置新的流末尾位置来截断这些字节或字符。  
  
> [!CAUTION]
>  如果将 **EOS** 设置为流的实际末尾之前的位置，则会丢失新的 **EOS** 位置之后的所有数据。  
  
## <a name="applies-to"></a>适用于  
 [流对象 (ADO)](./stream-object-ado.md)