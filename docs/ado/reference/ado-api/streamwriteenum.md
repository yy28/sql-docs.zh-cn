---
title: StreamWriteEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 37435758716d914b868e785eaaf72243de8ebbc6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否将行分隔符追加到字符串写入到[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|默认值。 写入指定的文本字符串 (由指定*数据*参数) 到**流**对象。|  
|**adWriteLine**|1|将文本字符串和行分隔符字符写入**流**对象。 如果[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)未定义属性，则这返回运行时错误。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
