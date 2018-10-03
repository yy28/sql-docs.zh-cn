---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0db8c7972d6b647cdd021d43dbb3cdee1ba0452
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678525"
---
# <a name="seteos-method"></a>SetEOS 方法
设置流的末尾的位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>备注  
 **SetEOS**的值更新[EOS](../../../ado/reference/ado-api/eos-property.md)属性，通过使当前[位置](../../../ado/reference/ado-api/position-property-ado.md)流的末尾。 任何字节或字符遵循当前的位置将被截断。  
  
 因为[编写](../../../ado/reference/ado-api/write-method.md)， [WriteText](../../../ado/reference/ado-api/writetext-method.md)，并[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)不会截断中现有的任何额外值**Stream**对象，您可以截断这些通过设置与新的流末尾位置的字符或字节**SetEOS**。  
  
> [!CAUTION]
>  如果您设置**EOS**到实际的流结束前的位置，则将所有数据都丢失后的新**EOS**位置。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
