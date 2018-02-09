---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e234d22e68d90819d73702542f7d3763ddd2f8c3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
指定用于打开选项[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。 值可以与或运算组合。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|打开**流**异步模式中的对象。|  
|**adOpenStreamFromRecord**|4|标识的内容*源*参数需要已打开[记录](../../../ado/reference/ado-api/record-object-ado.md)对象。 默认行为是将*源*作为直接指向树状结构中的节点的 URL。 打开与该节点关联的默认流。|  
|**adOpenStreamUnspecified**|-1|默认值。 指定打开**流**使用默认选项的对象。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [Open 方法（ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)
