---
title: Write 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 911a9dfb21c054dc95c54d9fb429d628d8e01fa4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764428"
---
# <a name="write-method"></a>Write 方法
向[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象写入二进制数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>参数  
 *宽限*  
 一个**变量**，包含要写入的字节数组。  
  
## <a name="remarks"></a>备注  
 指定的字节将写入**流**对象，而不会在每个字节之间插入空格。  
  
 [当前位置设置为写入](../../../ado/reference/ado-api/position-property-ado.md)数据之后的字节。 **写入**方法不会截断流中的其余数据。 如果要截断这些字节，请调用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果写入超过当前的[EOS](../../../ado/reference/ado-api/eos-property.md)位置，则会将**流**的[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)增加到包含任何新字节，而**EOS**会移动到**流**中的新最后一个字节。  
  
> [!NOTE]
>  **Write**方法用于二进制流（[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)为**adTypeBinary**）。 对于文本流（**类型**为**adTypeText**），请使用[WriteText](../../../ado/reference/ado-api/writetext-method.md)。  
  
## <a name="applies-to"></a>应用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
