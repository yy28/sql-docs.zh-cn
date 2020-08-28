---
description: StreamOpenOptionsEnum
title: StreamOpenOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f3865a3b0e550e7e3fe4887fb948bca72eadf1b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988498"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
指定用于打开 [流](./stream-object-ado.md) 对象的选项。 值可以与或运算结合使用。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|在异步模式下打开 **流** 对象。|  
|**adOpenStreamFromRecord**|4|将 *源* 参数的内容标识为已打开的 [记录](./record-object-ado.md) 对象。 默认行为是将 *源* 视为直接指向树结构中某个节点的 URL。 将打开与该节点关联的默认流。|  
|**adOpenStreamUnspecified**|-1|默认。 指定用默认选项打开 **流** 对象。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用于  
 [Open 方法（ADO 流）](./open-method-ado-stream.md)