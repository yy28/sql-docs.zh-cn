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
author: rothja
ms.author: jroth
ms.openlocfilehash: e609a51d6b9f42cb6101ff485633302193757fbd
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242647"
---
# <a name="locktypeenum"></a>LockTypeEnum
指定在编辑过程中放置在记录上的锁的类型。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|指示开放式批处理更新。 对于批处理更新模式是必需的。|  
|**adLockOptimistic**|3|指示开放式锁定，按记录记录。 提供程序使用开放式锁定，仅在调用[Update](../../../ado/reference/ado-api/update-method.md)方法时锁定记录。|  
|**adLockPessimistic**|2|指示悲观锁定，按记录记录。 提供程序执行必要的操作以确保成功编辑记录，通常是在编辑后直接在数据源中锁定记录。|  
|**adLockReadOnly**|1|指示只读记录。 不能更改数据。|  
|**adLockUnspecified**|-1|不指定锁的类型。 对于克隆，会创建克隆，其锁定类型与原始副本相同。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums. LockType|  
|AdoEnums. LockType|  
|AdoEnums. LockType|  
|AdoEnums. LockType。未指定|  
  
## <a name="applies-to"></a>应用到  

:::row:::
    :::column:::
        [Clone 方法 (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)  
        [LockType 属性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)  
    :::column-end:::
    :::column:::
        [Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)  
        [WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  
    :::column-end:::
:::row-end:::
