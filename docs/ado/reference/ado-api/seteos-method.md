---
title: "SetEOS 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 600625802c16c8e6860c462fe369f70eb9c1805c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="seteos-method"></a>SetEOS 方法
设置为流的末尾的位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>注释  
 **SetEOS**更新的值[EOS](../../../ado/reference/ado-api/eos-property.md)属性，通过使当前[位置](../../../ado/reference/ado-api/position-property-ado.md)流的末尾。 任何字节或字符当前位置后将被截断。  
  
 因为[编写](../../../ado/reference/ado-api/write-method.md)， [WriteText](../../../ado/reference/ado-api/writetext-method.md)，和[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)不会截断中现有的任何额外值**流**对象，你便可以截断这些字节或通过设置与新的最终的流位置的字符**SetEOS**。  
  
> [!CAUTION]
>  如果你设置**EOS**为之前的实际流末尾的位置，则将所有数据都丢失后新**EOS**位置。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
