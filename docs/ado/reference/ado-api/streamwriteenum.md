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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928633"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否将行分隔符追加到字符串写入到[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
|常量|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|默认值。 将指定的文本字符串写入 (通过指定*数据*参数) 到**Stream**对象。|  
|**adWriteLine**|1|将文本字符串和行分隔符字符写入**Stream**对象。 如果[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)未定义属性，则这返回运行时错误。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
