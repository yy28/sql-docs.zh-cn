---
title: sp_filestream_force_garbage_collection (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_filestream_force_garbage_collection
- sp_filestream_force_garbage_collection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILESTREAM [SQL Server]
- sp_filestream_force_garbage_collection
ms.assetid: 9d1efde6-8fa4-42ac-80e5-37456ffebd0b
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5cd74006b394f7412f7ec2d3c6bfacb36f701cf1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239327"
---
# <a name="spfilestreamforcegarbagecollection-transact-sql"></a>sp_filestream_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  强制运行 FILESTREAM 垃圾回收器，从而删除任何不需要的 FILESTREAM 文件。  
  
 在垃圾回收器清除 FILESTREAM 容器中的所有删除文件后，才能删除该容器。 FILESTREAM 垃圾回收器是自动运行的。 但是，如果你需要删除之前垃圾回收器的容器运行之后，你可以使用 sp_filestream_force_garbage_collection 手动运行垃圾回收器。  
  
  
## <a name="syntax"></a>语法  
  
```  
sp_filestream_force_garbage_collection  
    [ @dbname = ]  'database_name',  
    [ @filename = ] 'logical_file_name' ]  
```  
  
## <a name="arguments"></a>参数  
 **@dbname** = *database_name***'**  
 指示要运行垃圾回收器的数据库的名称。  
  
> [!NOTE]  
>  *dbname*是**sysname**。 如果未指定，则假定为当前数据库。  
  
 **@filename** = *logical_file_name*  
 指定要运行垃圾回收器的 FILESTREAM 容器的逻辑名称。 **@filename** 是可选的。 如果不指定了任何逻辑文件名，垃圾回收器将清除指定数据库中的所有 FILESTREAM 容器。  
  
## <a name="return-code-values"></a>返回代码值  
  
|||  
|-|-|  
|“值”|说明|  
|0|操作成功|  
|1|操作失败|  
  
## <a name="result-sets"></a>结果集  
  
|“值”|Description|  
|-----------|-----------------|  
|*file_name*|指示 FILESTREAM 容器名称|  
|*num_collected_items*|指示此容器中已回收（删除）的 FILESTREAM 项目（文件/目录）数。|  
|*num_marked_for_collection_items*|指示此容器中已标记为回收（删除）的 FILESTREAM 项目（文件/目录）数。 这些项尚未，尚未删除，但可能有资格获得删除以下垃圾收集阶段。|  
|*num_unprocessed_items*|指示此 FILESTREAM 容器中符合条件但未进行垃圾回收处理的 FILESTREAM 项目（文件或目录）数。 可能由于各种原因而未处理项目，其中包括：<br /><br /> 由于尚未执行日志备份或检查点操作，需要暂时锁定文件。<br /><br /> 文件处于 FULL 或 BULK_LOGGED 恢复模式。<br /><br /> 有长时间运行的活动事务。<br /><br /> 复制日志读取器作业未运行。 请参阅白皮书[SQL Server 2008 中的 FILESTREAM 存储](http://go.microsoft.com/fwlink/?LinkId=209156)有关详细信息。|  
|*last_collected_xact_seqno*|返回最后一个相应的日志序列号 (LSN)，已垃圾回收指定 FILESTREAM 容器中小于该编号的文件。|  
  
## <a name="remarks"></a>注释  
 在请求的数据库（和 FILESTREAM 容器）上显式运行 FILESTREAM 垃圾回收器任务，直至完成。 垃圾回收进程将删除不再需要的文件。 完成此操作所需的时间取决于该数据库或容器中的 FILESTREAM 数据大小，以及最近对 FILESTREAM 数据执行的 DML 活动的数量。 尽管可以在数据库联机时运行此操作，但这可能会在运行期间由于垃圾回收进程执行的各种 I/O 活动而影响数据库性能。  
  
> [!NOTE]  
>  建议仅在必要时运行此操作，并且在通常的工作时间以外运行。  
  
只能在单独容器或单独数据库上同时运行针对此存储过程的多个调用。  

由于两阶段操作，应运行存储的过程两次以实际删除基础 Filestream 文件。  

垃圾回收 (GC) 依赖于日志截断。 因此，如果使用完整恢复模式的数据库上，最近删除了文件，它们是 GC ed 只有在执行这些事务日志部分的日志备份和日志部分标记为不活动后。 在使用简单恢复模式的数据库之后, 将发生日志截断`CHECKPOINT`对数据库发出。  


## <a name="permissions"></a>权限  
 需要 db_owner 数据库角色中的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例为 `FSDB` 数据库中的 FILESTREAM 容器运行垃圾回收器。  
  
### <a name="a-specifying-no-container"></a>A. 不指定任何容器  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB';  
```  
  
### <a name="b-specifying-a-container"></a>B. 指定一个容器  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB',
    @filename = N'FSContainer';  
```  
  
## <a name="see-also"></a>另请参阅  
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 和 FileTable 动态管理视图 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 目录视图 (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (TRANSACT-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
  
