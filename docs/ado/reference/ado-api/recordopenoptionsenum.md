---
title: RecordOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c0ed637d8e77ef7fc152f994da81db010fa80900
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712159"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
指定用于打开选项[记录](../../../ado/reference/ado-api/record-object-ado.md)。 这些值可以组合使用或者。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|向与关联的字段的提供程序指示**记录**最初，不需要检索，但可以在首次尝试访问该字段进行检索。 此标志，缺少所指示的默认行为是检索所有**记录**对象字段。|  
|**adDelayFetchStream**|0x4000|向默认流与关联的提供程序指示**记录**最初不需要检索。 此标志，缺少所指示的默认行为是检索与关联的默认流**记录**对象。|  
|**adOpenAsync**|0x1000|指示**记录**在异步模式下打开对象。|  
|**adOpenExecuteCommand**|0x10000|指示源字符串包含应执行的命令文本。 此值相当于**adCmdText**选项卡上**Recordset.Open**。|  
|**adOpenRecordUnspecified**|-1|默认值。 指示未指定任何选项。|  
|**adOpenOutput**|0x800000|指示如果源指向包含一个可执行脚本的节点 (如。ASP 页面），然后打开**记录**将包含执行的脚本的结果。 此值才有效，且非集合记录。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)
