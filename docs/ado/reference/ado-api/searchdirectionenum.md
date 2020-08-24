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
ms.openlocfilehash: 13f8e73bc382493084c8d3712d4b7bda2ed35c13
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777526"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
指定记录 [集](./recordset-object-ado.md)内的记录搜索的方向。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|向后搜索，在 **记录集**的开头处停止。 如果找不到匹配项，则记录指针将置于 [BOF](./bof-eof-properties-ado.md)。|  
|**adSearchForward**|1|向前搜索，在 **记录集**末尾停止。 如果未找到匹配项，则记录指针定位于 [EOF](./bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>适用于  
 [Find 方法 (ADO)](./find-method-ado.md)