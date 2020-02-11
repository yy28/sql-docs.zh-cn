---
title: StreamWriteEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cc9de1481cc683bddafe2f92959977319600f6a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928633"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否将行分隔符追加到写入[流](../../../ado/reference/ado-api/stream-object-ado.md)对象的字符串。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|默认值。 向**流**对象写入指定的文本字符串（由*数据*参数指定）。|  
|**adWriteLine**|1|向**流**对象写入一个文本字符串和一个行分隔符。 如果未定义[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)属性，则会返回运行时错误。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>应用于  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
