---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8439f7d8fabc5675e43fca5bba006b22574b992
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931049"
---
# <a name="skipline-method"></a>SkipLine 方法
读取文本时，跳过整个一行[Stream](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>备注  
 将跳过所有字符，直至并包括下一步的行分隔符。 默认情况下[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)是**adCRLF**。 如果你尝试来试图跳过[EOS](../../../ado/reference/ado-api/eos-property.md)，将会保留在当前位置**EOS**。  
  
 **SkipLine**方法使用文本流 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
