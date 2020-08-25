---
description: SkipLine 方法
title: SkipLine 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
author: rothja
ms.author: jroth
ms.openlocfilehash: c0897d90ffeccabbce57525f268214577a523d92
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777466"
---
# <a name="skipline-method"></a>SkipLine 方法
读取文本 [流](./stream-object-ado.md)时，跳过整行。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>备注  
 将跳过所有字符，直到下一个行分隔符。 默认情况下， [LineSeparator](./lineseparator-property-ado.md) 为 **adCRLF**。 如果尝试跳过超过 [eos](./eos-property.md)，当前位置将保持在 **eos**。  
  
 **SkipLine**方法用于文本流 ([类型](./type-property-ado-stream.md)为**adTypeText**) 。  
  
## <a name="applies-to"></a>适用于  
 [流对象 (ADO)](./stream-object-ado.md)