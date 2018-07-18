---
title: LoadFromFile 方法 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 859c4cd31c3a2da8ff42fed470e5651ac568619b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35279269"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 方法 (ADO)
加载到现有文件的内容[流](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parameters  
 *FileName*  
 A**字符串**值，该值包含要加载到的文件的名称**流**。 *FileName*可以包含任何有效的路径和 UNC 格式的名称。 如果指定的文件不存在，则会发生运行时错误。  
  
## <a name="remarks"></a>Remarks  
 此方法可以用于加载到本地文件的内容**流**对象。 这可以用于将本地文件的内容上载到服务器。  
  
 **流**对象必须是已打开之前调用**LoadFromFile**。 此方法不会更改的绑定**流**对象; 它仍将绑定到 URL 指定的对象或**记录**与其**流**最初打开。  
  
 **LoadFromFile**将覆盖的当前内容**流**对象从文件中读取的数据。 中的任何现有字节**流**覆盖该文件的内容。 以下任何以前现有和剩余字节[EOS](../../../ado/reference/ado-api/eos-property.md)由**LoadFromFile**，将被截断。  
  
 调用了**LoadFromFile**，当前位置设置为开始**流**([位置](../../../ado/reference/ado-api/position-property-ado.md)为 0)。  
  
 由于可能到编码的流的开头添加 2 个字节，流的大小可能与从其加载文件的大小不完全匹配。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
