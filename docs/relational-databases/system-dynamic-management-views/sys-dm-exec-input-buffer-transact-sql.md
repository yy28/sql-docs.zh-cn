---
title: sys.dm_exec_input_buffer (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7746f0fb0e23bf3c02d27b82ce1cdc69eca54bf6
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43072758"
---
# <a name="sysdmexecinputbuffer-transact-sql"></a>sys.dm_exec_input_buffer (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

  返回有关语句提交到的实例信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
sys.dm_exec_input_buffer ( session_id , request_id )
```  
  
## <a name="arguments"></a>参数  
*session_id*  
执行要查找的批处理的会话 id。 *session_id*是**smallint**。 *session_id*可以从以下动态管理对象中获得：  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)   
  
*request_id*  
从 request_id [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。 *request_id*是**int**。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**event_type**|**nvarchar(256)**|在给定 spid 输入缓冲区中的事件的类型。|  
|**参数**|**smallint**|为该语句提供任何参数。|  
|**event_info**|**nvarchar(max)**|给定 spid 的输入缓冲区中的语句的文本。|  
  
## <a name="permissions"></a>Permissions  
 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如果用户具有 VIEW SERVER STATE 权限，用户将看到所有正在执行的会话的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 否则为用户会看到仅为当前会话。  
  
 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，如果用户是数据库所有者，用户将看到所有正在执行的会话上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]; 否则为用户会看到仅为当前会话。  
  
## <a name="remarks"></a>Remarks  
 此动态管理函数可以通过这样做，使用与 sys.dm_exec_sessions 或 sys.dm_exec_requests **CROSS APPLY**。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example"></a>A. 简单示例  
 下面的示例演示将会话 id (SPID) 和一个请求 id 传递给该函数。  
  
```sql  
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```  
  
### <a name="b-using-cross-apply-to-additional-information"></a>B. 使用交叉应用于的其他信息  
 下面的示例列出了具有大于 50 的会话 id 的会话输入的缓冲区。  
  
```sql  
SELECT es.session_id, ib.event_info   
FROM sys.dm_exec_sessions AS es  
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib  
WHERE es.session_id > 50;
GO
```  
  
## <a name="see-also"></a>请参阅  
 [与执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [DBCC INPUTBUFFER (Transact-SQL)](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
