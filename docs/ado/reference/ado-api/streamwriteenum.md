---
description: StreamWriteEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 343e5fd45a32e45cda342ab01feb64f379054486
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777156"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否将行分隔符追加到写入 [流](./stream-object-ado.md) 对象的字符串。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|默认。 将 *数据* 参数) 指定 (指定的文本字符串写入 **流** 对象。|  
|**adWriteLine**|1|向 **流** 对象写入一个文本字符串和一个行分隔符。 如果未定义 [LineSeparator](./lineseparator-property-ado.md) 属性，则会返回运行时错误。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用于  
 [WriteText 方法](./writetext-method.md)