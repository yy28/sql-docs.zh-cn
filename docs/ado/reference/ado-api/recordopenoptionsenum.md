---
title: RecordOpenOptionsEnum |Microsoft 文档
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
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0795d6eb942f10a97be1acda77954ae43fd4f2e4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281256"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
指定用于打开选项[记录](../../../ado/reference/ado-api/record-object-ado.md)。 这些值可能组合的使用或者。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|向字段与关联的提供程序指示**记录**最初，不需要检索，但可以在第一次尝试访问该字段检索。 缺少此标志，指示的默认行为是检索所有**记录**对象字段。|  
|**adDelayFetchStream**|0x4000|向关联的默认流时使用的提供程序指示**记录**最初不需要检索。 缺少此标志，指示的默认行为是检索与关联的默认流**记录**对象。|  
|**adOpenAsync**|0x1000|指示**记录**异步模式中打开对象。|  
|**adOpenExecuteCommand**|0x10000|指示源字符串包含应执行的命令文本。 此值相当于**adCmdText**选项**Recordset.Open**。|  
|**adOpenRecordUnspecified**|-1|默认值。 指示未指定任何选项。|  
|**adOpenOutput**|0x800000|如果源指向包含一个可执行的脚本的节点表示 (如。ASP 页面），然后打开**记录**将包含执行脚本的结果。 此值才有效，且非集合记录。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)
