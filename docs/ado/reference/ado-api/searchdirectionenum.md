---
title: SearchDirectionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f05af48f2edcdcf2c6adc6e3617860fdad38bde7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776154"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
指定的记录中搜索的方向[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|搜索向后，在开头处停止**记录集**。 如果找不到匹配项，在定位记录指针[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
|**adSearchForward**|1|向前搜索，在末尾处停止**记录集**。 如果找不到匹配项，在定位记录指针[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>适用范围  
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
