---
title: EventReasonEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 743e36e379760cb2c148c5484bb7b49b08d1d27e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644635"
---
# <a name="eventreasonenum"></a>EventReasonEnum
指定导致了事件发生的原因。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|操作添加一个新的记录。|  
|**adRsnClose**|9|操作关闭**记录集**。|  
|**adRsnDelete**|2|操作删除了记录。|  
|**adRsnFirstChange**|11|操作的记录所做的第一个更改。|  
|**adRsnMove**|10|操作将在记录指针**记录集**。|  
|**adRsnMoveFirst**|12|操作移动到中的第一个记录的记录指针**记录集**。|  
|**adRsnMoveLast**|15|操作移到最后一个记录中记录指针**记录集**。|  
|**adRsnMoveNext**|13|操作中的下一个记录将记录指针**记录集**。|  
|**adRsnMovePrevious**|14|操作移到上一记录中记录指针**记录集**。|  
|**adRsnRequery**|7|重新查询操作[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
|**adRsnResynch**|8|操作重新同步**记录集**与数据库。|  
|**adRsnUndoAddNew**|5|撤消删除操作添加一个新的记录。|  
|**adRsnUndoDelete**|6|撤消删除操作删除记录。|  
|**adRsnUndoUpdate**|4|撤消删除操作记录的更新。|  
|**adRsnUpdate**|3|操作更新现有记录。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
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
