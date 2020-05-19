---
title: Read 方法 |Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: rothja
ms.author: jroth
ms.openlocfilehash: 75b39b758d48a173bcfbe84e3fecbd20cce5ee12
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754263"
---
# <a name="read-method"></a>Read 方法
从二进制[流](../../../ado/reference/ado-api/stream-object-ado.md)对象中读取指定数目的字节。  
  
## <a name="syntax"></a>语法  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>参数  
 *NumBytes*  
 可选。 一个**长整型**值，指定要从文件中读取的字节数，或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值**adReadAll**（这是默认值）。  
  
## <a name="return-value"></a>返回值  
 **Read**方法从**流**对象读取指定数目的字节或整个流，并将生成的数据作为**变量**返回。  
  
## <a name="remarks"></a>备注  
 如果*NumBytes*大于**流**中剩余字节数，则仅返回剩余字节数。 不填充数据读取以匹配*NumBytes*指定的长度。 如果没有剩余字节可供读取，则返回具有 null 值的变量。 **读取**不能用于向后读取。  
  
> [!NOTE]
>  *NumBytes*始终度量字节。 对于文本**流**对象（[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)为**AdTypeText**），请使用[ReadText](../../../ado/reference/ado-api/readtext-method.md)。  
  
## <a name="applies-to"></a>应用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)
