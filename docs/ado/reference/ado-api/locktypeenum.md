---
title: LockTypeEnum |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918248"
---
# <a name="locktypeenum"></a>LockTypeEnum
指定在编辑过程中放置在记录上的锁的类型。  
  
|Constant|Value|说明|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|指示开放式批处理更新。 对于批处理更新模式是必需的。|  
|**adLockOptimistic**|3|指示开放式锁定，按记录记录。 提供程序使用开放式锁定，仅在调用[Update](../../../ado/reference/ado-api/update-method.md)方法时锁定记录。|  
|**adLockPessimistic**|2|指示悲观锁定，按记录记录。 提供程序执行必要的操作以确保成功编辑记录，通常是在编辑后直接在数据源中锁定记录。|  
|**adLockReadOnly**|1|指示只读记录。 不能更改数据。|  
|**adLockUnspecified**|-1|不指定锁的类型。 对于克隆，会创建克隆，其锁定类型与原始副本相同。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|Constant|  
|--------------|  
|AdoEnums. LockType. BATCHOPTIMISTIC|  
|AdoEnums. LockType|  
|AdoEnums. LockType|  
|AdoEnums. LockType|  
|AdoEnums. LockType。未指定|  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[Clone 方法 (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[LockType 属性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
