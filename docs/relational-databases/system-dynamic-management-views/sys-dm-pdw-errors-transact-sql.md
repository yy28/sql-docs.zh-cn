---
title: sys.dm_pdw_errors (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 57b6bd92ded85345dc1b716df2fa395df17fff02
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657121"
---
# <a name="sysdmpdwerrors-transact-sql"></a>sys.dm_pdw_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存所有请求或查询的执行过程中遇到的错误有关的信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|此视图的键。<br /><br /> 与错误关联的唯一数字 id。|跨系统中的所有查询错误是唯一的。|  
|源 (source)|**nvarchar(64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|type|**nvarchar(4000)**|发生的错误的类型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|发生错误的时间。|小于或等于当前时间。|  
|pwd_node_id|**int**|如果任何涉及的特定节点的标识符。 节点 id 的其他信息，请参阅[sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。||  
|session_id|**nvarchar(32)**|如果任何涉及的会话标识符。 会话 id 的其他信息，请参阅[sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|request_id|**nvarchar(32)**|如果任何涉及请求的标识符。 请求 id 的其他信息，请参阅[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。||  
|spid|**int**|如果任何涉及 SQL Server 会话的 spid。||  
|thread_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|详细信息|**nvarchar(4000)**|保存完整的错误文本说明。||  
  
 此视图按保留的最大行有关的信息，请参阅中的元数据部分[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主题。  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
