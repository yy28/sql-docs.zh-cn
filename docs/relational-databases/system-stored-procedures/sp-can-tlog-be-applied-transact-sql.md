---
title: sp_can_tlog_be_applied (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_can_tlog_be_applied_TSQL
- sp_can_tlog_be_applied
dev_langs:
- TSQL
helpviewer_keywords:
- sp_can_tlog_be_applied
ms.assetid: 9c143b6c-27ac-4ab7-98d1-3b7b265f3963
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f5e586112df85e44950abf17a8c874e83749bc2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spcantlogbeapplied-transact-sql"></a>sp_can_tlog_be_applied (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  验证事务日志备份是否可应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。 **sp_can_tlog_be_applied**需要该数据库处于 Restoring 状态。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_can_tlog_be_applied [ @backup_file_name = ] 'backup_file_name'   
        , [ @database_name = ] 'database_name'   
        , [ @result = ] result OUTPUT  
```  
  
## <a name="arguments"></a>参数  
 [ **@backup_file_name=** ] **'***backup_file_name***'**  
 备份文件的名称。 *backup_file_name*是**nvarchar （128)**。  
  
 [ **@database_name=** ] **'***database_name***'**  
 数据库的名称。 database_name 的数据类型为 sysname。  
  
 [  **@result=** ]*结果***输出**  
 指示事务日志是否可应用于数据库。 *结果*是**位**。  
  
 1 = 日志可以应用  
  
 0= 日志不能应用。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_can_tlog_be_applied**。  
  
## <a name="examples"></a>示例  
 以下示例将声明一个本地变量 `@MyBitVar`，用于存储结果。  
  
```  
USE master;  
GO  
DECLARE @MyBitVar BIT;  
EXEC sp_can_tlog_be_applied  
     @backup_file_name =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\AdventureWorks2012.bak',  
     @database_name = N'AdventureWorks2012',  
     @result = @MyBitVar OUTPUT;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
