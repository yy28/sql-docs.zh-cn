---
title: RecordCreateOptionsEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b632135977e07763f2c2f11c9c55cc5ee37e499
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
