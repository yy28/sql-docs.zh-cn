---
title: "PositionEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: PositionEnum
helpviewer_keywords: PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 006958663621ec4d226f756af6aad44c05f5a92e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="positionenum"></a>PositionEnum
指定在记录指针的当前位置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|该值指示当前记录指针是否在 BOF (即， [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性是**True**)。|  
|**adPosEOF**|-3|指示当前记录指针位于 EOF (即， [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性是**True**)。|  
|**adPosUnknown**|-1|指示**记录集**是空的当前的位置是未知的或提供程序不支持[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)或[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)属性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
