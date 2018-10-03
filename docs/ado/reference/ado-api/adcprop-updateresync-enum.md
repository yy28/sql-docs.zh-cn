---
title: ADCPROP_UPDATERESYNC_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afaadf62c38c318c759be1c452ff0953ba19c7d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615575"
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
指定是否[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法后跟一个隐式[重新同步](../../../ado/reference/ado-api/resync-method.md)方法操作，如果是，该操作的范围。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|调用**重新同步**与所有其他 ADCPROP_UPDATERESYNC_ENUM 成员的组合值。|  
|**adResyncAutoIncrement**|1|默认值。 尝试检索自动递增，或生成的数据源，例如 Microsoft Jet 自动编号字段或 Microsoft SQL Server 标识列的列的新标识值。|  
|**adResyncConflicts**|2|调用**重新同步**的 update 或 delete 操作因并发冲突而导致的失败的所有行。|  
|**adResyncInserts**|8|调用**重新同步**为所有成功插入的行。 但是，不重新同步自动递增列的值。 相反，新插入的行的内容进行重新同步基于现有的主键值。 如果主键是自动增量值，**重新同步**不会检索预期行的内容。 对于自动递增 AutoIncrement 主键值，调用**UpdateBatch**合并值与**adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|不会调用**重新同步**。|  
|**adResyncUpdates**|4|调用**重新同步**的所有已成功更新行。|  
  
## <a name="applies-to"></a>适用范围  
 [Update Resync 属性 - 动态 (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
