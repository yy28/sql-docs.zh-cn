---
title: "ADCPROP_UPDATERESYNC_ENUM |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords: ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 998868819c0e0b56783598ea3f2af5a3d799f82c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
指定是否[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法后跟一种隐式[重新同步](../../../ado/reference/ado-api/resync-method.md)方法操作，如果是，该操作的作用域。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|调用**重新同步**与所有其他 ADCPROP_UPDATERESYNC_ENUM 成员的合并值。|  
|**adResyncAutoIncrement**|1|默认值。 尝试检索自动递增，或生成的数据源，如 Microsoft Jet AutoNumber 字段或 Microsoft SQL Server 标识列的列的新标识值。|  
|**adResyncConflicts**|2|调用**重新同步**对于在其中更新或删除操作失败，因为并发冲突的所有行。|  
|**adResyncInserts**|8|调用**重新同步**对所有成功插入的行。 但是，不重新同步 AutoIncrement 列的值。 相反，新插入的行的内容会重新同步根据现有的主键值。 如果主键是 AutoIncrement 值，**重新同步**不会检索预期的行的内容。 对于自动递增 AutoIncrement 主键值，调用**UpdateBatch**的合并值与**adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|不会调用**重新同步**。|  
|**adResyncUpdates**|4|调用**重新同步**对于已成功更新的所有行。|  
  
## <a name="applies-to"></a>适用范围  
 [Update Resync 属性 - 动态 (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
