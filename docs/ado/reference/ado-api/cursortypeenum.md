---
description: CursorTypeEnum
title: CursorTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e0d37d5aad3f27a61cf3ae7c8dad9b27149e09b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775466"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
指定 [记录集](./recordset-object-ado.md) 对象中使用的游标类型。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|使用动态游标。 其他 **用户的添加** 、更改和删除是可见的，并且允许所有类型的移动（书签除外，如果提供程序不支持）。|  
|**adOpenForwardOnly**|0|默认。 使用只进游标。 与静态游标相同，不同之处在于只能向前滚动记录。 当只需通过 **记录集**进行一次传递时，这可以提高性能。|  
|**adOpenKeyset**|1|使用键集游标。 与动态游标类似，但你看不到其他用户添加的记录，但其他用户删除的记录无法从 **记录集中**访问。 其他用户的数据更改仍然可见。|  
|**adOpenStatic**|3|使用静态游标，该游标是一组记录的静态副本，可用于查找数据或生成报表。 其他用户的添加、更改或删除不可见。|  
|**adOpenUnspecified**|-1|不指定游标的类型。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums. CursorType|  
|AdoEnums. CursorType. FORWARDONLY|  
|AdoEnums. CursorType|  
|AdoEnums. CursorType|  
|AdoEnums. CursorType。未指定|  
  
## <a name="applies-to"></a>适用于  
 [CursorType 属性 (ADO)](./cursortype-property-ado.md)