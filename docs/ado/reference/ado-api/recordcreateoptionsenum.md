---
title: RecordCreateOptionsEnum | Microsoft Docs
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
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c36b34f0d8eabdde75b25847d1ae47c674af2e6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
指定是否现有**记录**应打开或新**记录**为创建[记录](../../../ado/reference/ado-api/record-object-ado.md)对象[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 可以使用 AND 运算符组合的值。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|创建一个新**记录**在指定的节点*源*参数，而不是打开的现有**记录**。 如果源指向现有节点中，就会发生运行时错误，除非**adCreateCollection**与结合**adOpenIfExists**或**adCreateOverwrite**。|  
|**adCreateNonCollection**|0|创建一个新**记录**类型的[adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md)。|  
|**adCreateOverwrite**|0x4000000|修改创建标志**adCreateCollection**， **adCreateNonCollection**，和**adCreateStructDoc**。 时或如果源 URL 指向的现有节点与此值，并创建标志值，一个使用或**记录**，则现有**记录**不覆盖，因此新的位置中创建的一个。 此值不能使用连同**adOpenIfExists**。|  
|**adCreateStructDoc**|0x80000000|创建一个新**记录**类型的[adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md)，而不是打开的现有**记录**。|  
|**adFailIfNotExists**|-1|默认值。 如果将导致运行时错误*源*指向不存在节点。|  
|**adOpenIfExists**|0x2000000|修改创建标志**adCreateCollection**， **adCreateNonCollection**，和**adCreateStructDoc**。 时或如果源 URL 指向的现有节点与此值，并创建标志值，一个使用或**记录**对象，然后提供程序必须打开现有**记录**而不是创建一个新一个。 此值不能使用连同**adCreateOverwrite**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)
