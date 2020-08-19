---
description: SearchDirectionEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 918261998fec061f8f977a8a2dfc614166f564f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442159"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
指定记录 [集](../../../ado/reference/ado-api/recordset-object-ado.md)内的记录搜索的方向。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|向后搜索，在 **记录集**的开头处停止。 如果找不到匹配项，则记录指针将置于 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
|**adSearchForward**|1|向前搜索，在 **记录集**末尾停止。 如果未找到匹配项，则记录指针定位于 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>适用于  
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
