---
title: CursorTypeEnum | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dd3469b826ac4f577ff0e883b1a92a3acec4a981
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698532"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
指定的游标中使用的类型[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|使用动态游标。 添加、 更改和删除操作的其他用户是可见的并且所有类型的通过移动**记录集**都允许，书签除外，如果提供程序不支持它们。|  
|**adOpenForwardOnly**|0|默认值。 使用只进游标。 与静态游标相同，只不过您可以仅向前滚动记录。 这样可以提高性能，当您需要只进行一次传递时**记录集**。|  
|**adOpenKeyset**|1|使用由键集游标。 与动态游标，相似，只不过您无法看到其他用户添加、 的记录，尽管其他用户删除的记录从无法访问你**记录集**。 由其他用户的数据更改才会仍然可见。|  
|**adOpenStatic**|3|使用静态游标，这是一组可用于查找数据或生成报告的记录的静态副本。 添加、 更改或删除其他用户不可见。|  
|**adOpenUnspecified**|-1|不会指定游标的类型。|  
  
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
