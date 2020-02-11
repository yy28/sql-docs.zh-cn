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
ms.openlocfilehash: f8926e932317096cb3891cc8c480164268751cea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917001"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
指定记录[集](../../../ado/reference/ado-api/recordset-object-ado.md)内的记录搜索的方向。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|向后搜索，在**记录集**的开头处停止。 如果找不到匹配项，则记录指针将置于[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
|**adSearchForward**|1|向前搜索，在**记录集**末尾停止。 如果未找到匹配项，则记录指针定位于[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|一直|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>应用于  
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
