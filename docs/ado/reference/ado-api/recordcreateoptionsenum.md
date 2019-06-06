---
title: RecordCreateOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d57f1bc241e5e27618a9598895ea7be089ce20dd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712013"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
指定是否将现有**记录**应为打开或一个新**记录**为创建[记录](../../../ado/reference/ado-api/record-object-ado.md)对象[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 可以使用 AND 运算符组合这些值。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|创建一个新**记录**在指定的节点*源*参数，而不是打开的现有**记录**。 如果源指向现有节点，则会出现运行时错误，除非**adCreateCollection**结合**adOpenIfExists**或**adCreateOverwrite**。|  
|**adCreateNonCollection**|0|创建一个新**记录**类型的[adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md)。|  
|**adCreateOverwrite**|0x4000000|修改创建标志**adCreateCollection**， **adCreateNonCollection**，并**adCreateStructDoc**。 时或如果源 URL 指向的现有节点使用此值和一个创建标志值，或**记录**，则现有**记录**已覆盖以及新在其原位置创建一个。 不能使用此值连同**adOpenIfExists**。|  
|**adCreateStructDoc**|0x80000000|创建一个新**记录**类型的[adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md)，而不是打开的现有**记录**。|  
|**adFailIfNotExists**|-1|默认值。 如果会导致运行时错误*源*指向不存在节点。|  
|**adOpenIfExists**|0x2000000|修改创建标志**adCreateCollection**， **adCreateNonCollection**，并**adCreateStructDoc**。 当使用与此值和一个创建标志值，如果源 URL 指向的现有节点或**记录**对象，则提供程序必须打开现有**记录**而不是创建一个新其中一个。 不能使用此值连同**adCreateOverwrite**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)
