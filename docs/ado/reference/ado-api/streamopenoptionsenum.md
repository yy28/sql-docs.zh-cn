---
title: StreamOpenOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 562e79590a2a5f1f5e9bb609b9a0ad0ea8b2bfd9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928685"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
指定用于打开选项[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。 可以使用或运算组合的值。  
  
|常量|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|此时将打开**Stream**在异步模式下的对象。|  
|**adOpenStreamFromRecord**|4|标识的内容*源*参数是已打开[记录](../../../ado/reference/ado-api/record-object-ado.md)对象。 默认行为是将视为*源*作为 URL 直接指向树状结构中的节点。 打开与该节点关联的默认流。|  
|**adOpenStreamUnspecified**|-1|默认值。 指定左**Stream**对象使用默认选项。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [Open 方法（ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)
