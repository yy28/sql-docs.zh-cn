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
ms.openlocfilehash: 939de5306982ab2e369fce0648e477cac5f48cb8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441789"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否将行分隔符追加到写入 [流](../../../ado/reference/ado-api/stream-object-ado.md) 对象的字符串。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|默认。 将 *数据* 参数) 指定 (指定的文本字符串写入 **流** 对象。|  
|**adWriteLine**|1|向 **流** 对象写入一个文本字符串和一个行分隔符。 如果未定义 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 属性，则会返回运行时错误。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用于  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
