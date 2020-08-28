---
description: SkipLine 方法
title: SkipLine 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 840c0111aca8b202fd081d3f0250d17fd43e5bbb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989048"
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