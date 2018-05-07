---
title: DISCOVER_LOCKS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c835183f85f72046c3a20ccdee6478ed5661e015
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="discoverlocks-rowset"></a>DISCOVER_LOCKS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供有关服务器上的当前持续锁定的信息。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_LOCKS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LOCK_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||请求锁定时的 UTC 服务器时间。|  
|**LOCK_GRANT_TIME**|**DBTYPE_DBTIMESTAMP**||对资源授予锁时的 UTC 服务器时间。|  
|**LOCK_ID**|**DBTYPE_GUID**||锁的唯一标识符，以 GUID 形式表示。|  
|**LOCK_OBJECT_ID**|**DBTYPE_WSTR**||被锁定的对象的唯一标识符。|  
|**LOCK_STATUS**|**DBTYPE_I4**||锁定状态中。<br /><br /> 0 表示“等待锁定对象”。<br /><br /> 1 表示“已授予锁”。|  
|**LOCK_TRANSACTION_ID**|**DBTYPE_GUID**||事务的唯一标识符，以 GUID 形式表示。|  
|**锁类型**|**DBTYPE_I4**||锁类型的位掩码；有关详细信息，请参阅本主题的“备注”部分。|  
|**SPID**|**DBTYPE_I4**||会话 ID。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_LOCKS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|選擇性。|  
|LOCK_TRANSACTION_ID|DBTYPE_GUID|選擇性。|  
|LOCK_OBJECT_ID|DBTYPE_WSTR|選擇性。|  
|LOCK_STATUS|DBTYPE_I4|選擇性。|  
|LOCK_TYPE|DBTYPE_I4|選擇性。|  
|LOCK_MIN_TOTAL_MS|DBTYPE_I8|選擇性。|  
  
## <a name="remarks"></a>注释  
  
## <a name="lock-types"></a>锁类型  
  
|锁名称|“值”|Description|  
|---------------|-----------|-----------------|  
|LOCK_NONE|0x0000000|无锁。|  
|LOCK_SESSION_LOCK|0x0000001|不活动的会话；不影响其他锁。|  
|LOCK_READ|0x0000002|处理期间读取锁。|  
|LOCK_WRITE|0x0000004|处理期间写入锁。|  
|LOCK_COMMIT_READ|0x0000008|提交锁，共享。|  
|LOCK_COMMIT_WRITE|0x0000010|提交锁，排他。|  
|LOCK_COMMIT_ABORTABLE|0x0000020|提交过程中中止。|  
|LOCK_COMMIT_INPROGRESS|0x0000040|正在提交。|  
|LOCK_INVALID|0x0000080|无效的锁。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
