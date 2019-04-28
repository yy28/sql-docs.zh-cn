---
title: LoadFromFile 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed02b621b79ebf46dbb0dc6e66a2e5366610a19d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864401"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 方法 (ADO)
加载到现有文件的内容[Stream](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parameters  
 *FileName*  
 一个**字符串**值，该值包含要加载到的文件的名称**Stream**。 *文件名*可以包含任何有效的路径和名称以 UNC 格式。 如果指定的文件不存在，则会发生运行时错误。  
  
## <a name="remarks"></a>备注  
 此方法可用于加载到本地文件的内容**Stream**对象。 这可以用于将本地文件的内容上载到服务器。  
  
 **Stream**的对象必须是已打开之前调用**LoadFromFile**。 此方法不会更改的绑定**Stream**对象; 它仍将绑定到指定 URL 的对象或**记录**与其**Stream**最初是打开。  
  
 **LoadFromFile**的当前内容将覆盖**Stream**对象从文件中读取的数据。 中的任何现有字节**Stream**文件的内容被覆盖。 以下任何以前现有和剩余字节数[EOS](../../../ado/reference/ado-api/eos-property.md)创建的**LoadFromFile**，将被截断。  
  
 在调用**LoadFromFile**，当前的位置设置为开头**Stream** ([位置](../../../ado/reference/ado-api/position-property-ado.md)为 0)。  
  
 因为可能会在 2 个字节添加到编码流的开头，流的大小可能与从其加载的文件的大小不完全匹配。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
