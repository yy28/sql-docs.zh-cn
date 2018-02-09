---
title: EventReasonEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a49c3aac3b2f37421df9a68ae01b16770c696993
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="eventreasonenum"></a>EventReasonEnum
指定导致事件发生的原因。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|操作添加一条新记录。|  
|**adRsnClose**|9|操作关闭**记录集**。|  
|**adRsnDelete**|2|操作删除了记录。|  
|**adRsnFirstChange**|11|操作的记录所做的第一个更改。|  
|**adRsnMove**|10|操作将在记录指针**记录集**。|  
|**adRsnMoveFirst**|12|操作移动到中的第一个记录的记录指针**记录集**。|  
|**adRsnMoveLast**|15|操作移动到中的最后一个记录的记录指针**记录集**。|  
|**adRsnMoveNext**|13|操作移动到下一条记录的记录指针**记录集**。|  
|**adRsnMovePrevious**|14|操作移动到在上一记录的记录指针**记录集**。|  
|**adRsnRequery**|7|操作重新查询[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
|**adRsnResynch**|8|操作重新同步**记录集**与数据库。|  
|**adRsnUndoAddNew**|5|添加一条新记录撤消删除操作。|  
|**adRsnUndoDelete**|6|操作恢复删除的记录。|  
|**adRsnUndoUpdate**|4|撤消删除操作的记录更新。|  
|**adRsnUpdate**|3|操作更新现有记录。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package: **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.EventReason.ADDNEW|  
|AdoEnums.EventReason.CLOSE|  
|AdoEnums.EventReason.DELETE|  
|AdoEnums.EventReason.FIRSTCHANGE|  
|AdoEnums.EventReason.MOVE|  
|AdoEnums.EventReason.MOVEFIRST|  
|AdoEnums.EventReason.MOVELAST|  
|AdoEnums.EventReason.MOVENEXT|  
|AdoEnums.EventReason.MOVEPREVIOUS|  
|AdoEnums.EventReason.REQUERY|  
|AdoEnums.EventReason.RESYNCH|  
|AdoEnums.EventReason.UNDOADDNEW|  
|AdoEnums.EventReason.UNDODELETE|  
|AdoEnums.EventReason.UNDOUPDATE|  
|AdoEnums.EventReason.UPDATE|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[WillChangeRecord 和 RecordChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillMove 和 MoveComplete 事件 (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)||
