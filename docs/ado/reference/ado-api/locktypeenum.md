---
title: "LockTypeEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d1918f82bfe2361a90ca6f2479934ae1deba7664
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="locktypeenum"></a>LockTypeEnum
指定的编辑期间在记录上放置的锁的类型。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|指示开放式批量更新。 批处理更新模式，所需。|  
|**adLockOptimistic**|3|指示乐观锁定，记录的记录。 提供程序使用乐观锁定，锁定记录，仅在调用[更新](../../../ado/reference/ado-api/update-method.md)方法。|  
|**adLockPessimistic**|2|指示悲观锁定，记录的记录。 提供程序执行必要的操作以确保成功编辑的记录，通常通过编辑后立即锁定数据源中的记录。|  
|**adLockReadOnly**|1|指示只读的记录。 无法更改的数据。|  
|**adLockUnspecified**|-1|未指定锁的类型。 克隆，具有相同的锁类型与原始创建克隆。|  
  
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
|[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|

