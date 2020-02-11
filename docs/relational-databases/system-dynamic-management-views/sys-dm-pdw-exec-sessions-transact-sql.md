---
title: sys. dm_pdw_exec_sessions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/22/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4d559f7fb03b632fc5cfca573b2fedc72506fead
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899411"
---
# <a name="sysdm_pdw_exec_sessions-transact-sql"></a>sys. dm_pdw_exec_sessions （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关设备上当前或最近打开的所有会话的信息。 每个会话在表中各占一行。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar （32）**|当前查询或上次查询运行的 id （如果会话已终止，查询在终止时执行）。 此视图的键。|在系统中的所有会话中是唯一的。|  
|status|**nvarchar （10）**|对于当前会话，确定会话当前处于活动状态还是处于空闲状态。 对于过去的会话，会话状态可能显示为 "已关闭" 或 "已终止" （如果已强行关闭该会话）。|"活动"、"已关闭"、"空闲"、"已终止"|  
|request_id|**nvarchar （32）**|当前查询或上次查询运行的 id。|系统中所有请求都是唯一的。 如果未运行任何，则为 Null。|  
|security_id|**varbinary （85）**|运行会话的主体的安全 ID。||  
|login_name|**nvarchar(128)**|运行会话的主体的登录名。|符合用户命名约定的任何字符串。|  
|login_time|**datetime**|用户登录的日期和时间，创建此会话的日期和时间。|当前时间之前有效的**日期**时间。|  
|query_count|**int**|捕获自创建后运行的查询/requeststhis 会话数。|大于或等于0。|  
|is_transactional|**bit**|捕获会话当前是否在事务中。|对于自动提交，为 0; 对于事务，则为1。|  
|client_id|**nvarchar(255)**|捕获会话的客户端信息。|任何有效的字符串。|  
|app_name|**nvarchar(255)**|捕获应用程序名称信息，可以选择在连接过程中进行设置。|任何有效的字符串。|  
|sql_spid|**int**|SPID 的 id 号。 使用`session_id`此会话。 使用`sql_spid`列联接到**sys.databases dm_pdw_nodes_exec_sessions**。<br /><br /> ** \*警告\* \* **此列包含已关闭的 Spid。||  
  
 有关此视图保留的最大行的信息，请参阅[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主题中的元数据部分。  
  
## <a name="permissions"></a>权限  
 需要 `VIEW SERVER STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
