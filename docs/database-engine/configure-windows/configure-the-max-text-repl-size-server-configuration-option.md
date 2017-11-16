---
title: "配置“最大文本 REPL 大小”服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: max text repl size option
ms.assetid: 3056cf64-621d-4996-9162-3913f6bc6d5b
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2c08baba5a7b42249143b319f20f3d295fbee723
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-max-text-repl-size-server-configuration-option"></a>配置 max text repl size 服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本主题说明如何使用 **或** 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中配置 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] max text repl size [!INCLUDE[tsql](../../includes/tsql-md.md)]服务器配置选项。 **max text repl size** 选项指定使用单个 INSERT、UPDATE、WRITETEXT 或 UPDATETEXT 语句可以向已复制列或已捕获列添加的 **text****ntext****varchar(max)****nvarchar(max)****varbinary(max)****xml** 和 **image** 数据的最大大小（以字节为单位）。 默认值为 65536 个字节。 值为 -1 表示除了数据类型指定的限制之外，没有大小限制。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **配置 max text repl size 选项，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：**[在配置 max text repl size 选项之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   此选项适用于事务复制和变更数据捕获。 当将服务器配置为具有事务复制功能和变更数据捕获功能时，指定的值将适用于这两项功能。 快照复制和合并复制将会忽略此选项。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要执行带两个参数的 **sp_configure** 以更改配置选项或运行 RECONFIGURE 语句，则用户必须具备 ALTER SETTINGS 服务器级别的权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-max-text-repl-size-option"></a>配置 max text repl size 选项  
  
1.  在对象资源管理器中，右键单击“服务器”并选择“属性”。  
  
2.  单击 **“高级”** 节点。  
  
3.  在 **“杂项”**下，将 **“最大文本复制大小”** 选项更改为所需的值。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-max-text-repl-size-option"></a>配置 max text repl size 选项  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此示例说明如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 将 `max text repl size` 选项的值配置为 `-1`。  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;   
RECONFIGURE ;   
GO  
EXEC sp_configure 'max text repl size', -1 ;   
GO  
RECONFIGURE;   
GO  
  
```  
  
 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)服务器配置选项。  
  
##  <a name="FollowUp"></a> 跟进：在配置 max text repl size 选项之后  
 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>另请参阅  
 [复制功能和任务](../../relational-databases/replication/replication-features-and-tasks.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [UPDATETEXT (Transact-SQL)](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)  
  
  
