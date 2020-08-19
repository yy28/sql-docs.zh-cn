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
ms.openlocfilehash: 463de3740ce29b859732c5ddb7ba69d58069f93f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442091"
---
# <a name="skipline-method"></a>SkipLine 方法
读取文本 [流](../../../ado/reference/ado-api/stream-object-ado.md)时，跳过整行。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>备注  
 将跳过所有字符，直到下一个行分隔符。 默认情况下， [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 为 **adCRLF**。 如果尝试跳过超过 [eos](../../../ado/reference/ado-api/eos-property.md)，当前位置将保持在 **eos**。  
  
 **SkipLine**方法用于文本流 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)为**adTypeText**) 。  
  
## <a name="applies-to"></a>适用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
