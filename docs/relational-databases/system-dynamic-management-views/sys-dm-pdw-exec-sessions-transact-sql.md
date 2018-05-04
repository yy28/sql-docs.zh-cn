---
title: sys.dm_pdw_exec_sessions (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4b2546b76f266c4e3cc4fc16e1320bf409d8ea60
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含当前或最近打开设备上的所有会话有关的信息。 它列出每个会话的一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|当前的查询或运行 （如果终止该会话，并且已在终止时执行查询） 的最后一个查询的 id。 此视图的键。|跨系统中的所有会话唯一。|  
|status|**nvarchar(10)**|对于当前会话，标识是否会话当前处于活动状态还是空闲。 对于过去会话，状态可能会显示在会话关闭或终止 （如果强行关闭会话）。|'ACTIVE'、 已关闭，空闲，终止|  
|request_id|**nvarchar(32)**|当前的查询或运行的最后一个查询的 id。|唯一跨系统中的所有请求。 如果运行任何为 null。|  
|security_id|**varbinary(85)**|运行会话的主体的安全 ID。||  
|login_name|**nvarchar(128)**|运行会话的主体登录名。|任何符合的用户命名约定的字符串。|  
|login_time|**datetime**|创建日期和时间的用户登录和此会话。|有效**datetime**在当前时间之前。|  
|query_count|**int**|捕获自创建以来运行的查询/请求此会话数。|大于或等于 0。|  
|is_transactional|**bit**|捕获会话是否为当前在事务中或不。|自动提交的 0，1 表示事务。|  
|client_id|**nvarchar(255)**|捕获会话的客户端信息。|任何有效的字符串。|  
|app_name|**nvarchar(255)**|捕获应用程序名称信息 （可选） 设置为在连接过程的一部分。|任何有效的字符串。|  
|sql_spid|**int**|SPID id 号。 使用`session_id`此会话。 使用`sql_spid`列联接到**sys.dm_pdw_nodes_exec_sessions**。<br /><br /> **\*\* 警告\* \*** 此列包含已关闭的 Spid。||  
  
 有关通过此视图保留最大行数的信息，请参阅中的最大的系统视图值部分[最小值和最大值 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)主题。  
  
## <a name="permissions"></a>权限  
 需要 `VIEW SERVER STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
