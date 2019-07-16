---
title: LockTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ae822794b1b06a975e1cc3cd397b5a5f00036dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918248"
---
# <a name="locktypeenum"></a>LockTypeEnum
指定锁，在编辑期间放置在记录的类型。  
  
|常量|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|表示开放式批量更新。 所需的批更新模式。|  
|**adLockOptimistic**|3|指示乐观锁定，记录的记录。 提供程序使用乐观锁定，锁定记录仅在调用[更新](../../../ado/reference/ado-api/update-method.md)方法。|  
|**adLockPessimistic**|2|指示悲观锁定，记录的记录。 提供程序执行必要的以确保成功编辑的记录，通常通过编辑后立即锁定记录在数据源。|  
|**adLockReadOnly**|1|指示只读的记录。 不能更改的数据。|  
|**adLockUnspecified**|-1|不会指定锁的类型。 对于克隆，具有相同的锁类型与原始创建克隆。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums.LockType.OPTIMISTIC|  
|AdoEnums.LockType.PESSIMISTIC|  
|AdoEnums.LockType.READONLY|  
|AdoEnums.LockType.UNSPECIFIED|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[Clone 方法 (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[LockType 属性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
