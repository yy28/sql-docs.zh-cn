---
title: "StreamWriteEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 586920fc4f7673f9c5e25c92f252013920acaa8d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否将行分隔符追加到字符串写入到[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|默认值。 写入指定的文本字符串 (由指定*数据*参数) 到**流**对象。|  
|**adWriteLine**|1|将文本字符串和行分隔符字符写入**流**对象。 如果[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)未定义属性，则这返回运行时错误。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)

