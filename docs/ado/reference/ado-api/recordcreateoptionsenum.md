---
description: RecordCreateOptionsEnum
title: RecordCreateOptionsEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ef305aefbd3c606f433bfd85b1b10ac2dd94db1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442469"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
指定是打开现有**记录**还是为[记录](../../../ado/reference/ado-api/record-object-ado.md)对象[Open](../../../ado/reference/ado-api/open-method-ado-record.md)方法创建新**记录**。 值可以与 AND 运算符组合。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|在*Source*参数指定的节点上创建一个新**记录**，而不是打开现有**记录**。 如果源指向某个现有节点，则会发生运行时错误，除非将 **adCreateCollection** 与 **adOpenIfExists** 或 **adCreateOverwrite**组合在一起。|  
|**adCreateNonCollection**|0|创建[adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md)类型的新**记录**。|  
|**adCreateOverwrite**|0x4000000|修改创建标志 **adCreateCollection**、 **adCreateNonCollection**和 **adCreateStructDoc**。 当或与此值和创建标志值之一一起使用时，如果源 URL 指向现有的节点或 **记录**，则会覆盖现有记录，并在其位置创建一个新 **记录** 。 此值不能与 **adOpenIfExists**一起使用。|  
|**adCreateStructDoc**|0x80000000|创建[adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md)类型的新**记录**，而不是打开现有**记录**。|  
|**adFailIfNotExists**|-1|默认。 如果 *源* 指向不存在的节点，则会导致运行时错误。|  
|**adOpenIfExists**|0x2000000|修改创建标志 **adCreateCollection**、 **adCreateNonCollection**和 **adCreateStructDoc**。 当或与此值和创建标志值之一一起使用时，如果源 URL 指向现有的节点或 **记录** 对象，则提供程序必须打开现有的记录，而不是创建新的 **记录** 。 此值不能与 **adCreateOverwrite**一起使用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用于  
 [Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)
