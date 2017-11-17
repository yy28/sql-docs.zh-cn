---
title: "DBCC INPUTBUFFER (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
caps.latest.revision: 51
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 54e4c8309c290255cb2885fab04bb394bc453046
ms.openlocfilehash: 3d9b6acfbfef3125d6ee715708492de1cae2b3a2
ms.contentlocale: zh-cn
ms.lasthandoff: 10/16/2017

---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

显示从客户端发送到的实例的最后一个语句[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
*session_id*  
与各活动主连接关联的会话 ID。  
  
*request_id*  
要在当前会话中搜索的精确请求（批）。  

以下查询将返回*request_id*:  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
替换为  
启用要指定的选项。  
  
NO_INFOMSGS  
取消严重级别从 0 到 10 的所有信息性消息。  
  
## <a name="result-sets"></a>结果集  
DBCC INPUTBUFFER 返回包含如下列的行集。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**事件类型**|**nvarchar (30)**|事件类型。 这可能是**RPC 事件**或**语言事件**。 输出将为**否事件**时检测到没有最后一个事件。|  
|**参数**|**int**|0 = 文本<br /><br /> 1-  *n*  = 参数|  
|**EventInfo**|**nvarchar(4000)**|有关**EventType**的 RPC， **EventInfo**仅包含过程名称。 有关**EventType**的语言中，显示仅事件前 4000 个字符。|  
  
例如，当缓冲区中的最后一个事件是 DBCC INPUTBUFFER(11) 时，DBCC INPUTBUFFER 将返回以下结果集。
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> 从开始[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2，使用[sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)返回有关语句提交到的实例信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

## <a name="permissions"></a>Permissions  
上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要以下项之一：
-   用户必须是属于**sysadmin**固定的服务器角色。  
-   用户必须具有 VIEW SERVER STATE 权限。  
-   *session_id*必须在其运行该命令的会话 ID 相同。 要确定会话 ID，请执行以下查询：  
  
```sql
SELECT @@spid;  
```
  
上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]高级层需要 VIEW DATABASE STATE 权限的数据库中。 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]标准版和基本层需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]管理员帐户。
  
## <a name="examples"></a>示例  
以下示例在一个连接上运行一个时间较长的事务，而与此同时在另一个连接上运行 `DBCC INPUTBUFFER`。
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.dm_exec_input_buffer &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  

