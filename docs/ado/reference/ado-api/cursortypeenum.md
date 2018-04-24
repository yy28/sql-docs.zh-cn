---
title: CursorTypeEnum |Microsoft 文档
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
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4da9f1f931a9f6d15c5b0e13959f0e9effd40bcc
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="cursortypeenum"></a>CursorTypeEnum
指定的类型中使用的游标[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|使用动态游标。 添加、 更改和删除由其他用户均可见，并且所有类型的通过移动**记录集**允许中，书签除外，如果提供程序不支持它们。|  
|**adOpenForwardOnly**|0|默认值。 使用只进游标。 相同静态游标，只不过你可以仅向前滚动记录。 这提高了性能，你需要进行只有一个传递时**记录集**。|  
|**adOpenKeyset**|1|使用键集游标。 与动态游标，相似，只不过您无法看到其他用户将添加的记录，尽管其他用户删除的记录不可从你**记录集**。 由其他用户的数据更改是仍将可见。|  
|**adOpenStatic**|3|使用静态游标，这是一组可用于查找数据或生成报表的记录的静态副本。 添加、 更改或删除其他用户不可见。|  
|**adOpenUnspecified**|-1|未指定游标的类型。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>适用范围  
 [CursorType 属性 (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
