---
title: sp_updatestats (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0f10122f44768dd19f08f17ca9b2a12136be754f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  对当前数据库中所有用户定义表和内部表运行 UPDATE STATISTICS。  
  
 有关更新统计信息的详细信息，请参阅[更新统计信息&#40;TRANSACT-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)。 有关统计信息的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
    
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="arguments"></a>参数  
 [ **@resample** =]**对重新取样**  
 指定**sp_updatestats**将使用的重新取样选项[更新统计信息](../../t-sql/statements/update-statistics-transact-sql.md)语句。 如果**对重新取样**未指定， **sp_updatestats**通过使用默认采样来更新统计信息。 **对重新取样**是**varchar(8)** 默认值为 no。  
  
## <a name="remarks"></a>注释  
 **sp_updatestats**通过指定数据库中的所有用户定义和内部表上的所有关键字，来执行更新统计信息。 sp_updatestats 显示消息，以表明其进度。 完成更新之后，此存储过程将报告已为所有的表更新了统计信息。  
  
 sp_updatestats 更新已禁用非聚集索引的统计信息，但不更新已禁用聚集索引的统计信息。  
  
 对于基于磁盘的表， **sp_updatestats**更新统计信息基于**modification_counter**中的信息**sys.dm_db_stats_properties**目录视图，更新统计信息在至少一个该行已被修改。 内存优化表的统计信息在执行时始终更新**sp_updatestats**。 因此不会执行**sp_updatestats**只在必要时。  
  
 **sp_updatestats**可以触发重新编译的存储的过程或其他已编译的代码。 但是， **sp_updatestats**可能不会导致重新编译，如果只有一个查询计划所引用的表和它们的索引。 在这些情况下，即便更新了统计信息也不必进行重新编译。  
  
 数据库兼容性级别为 90，执行以下**sp_updatestats**不保留特定的统计信息的最新 NORECOMPUTE 设置。 对于兼容性级别为 90 或更高版本的数据库，sp_updatestats 未保留特定的统计信息的最新 NORECOMPUTE 选项。 有关禁用和重新启用统计信息更新的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定服务器角色或数据库的所有权 (**dbo**)。  
  
## <a name="examples"></a>示例  
 以下示例更新 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中各表的统计信息。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS (Transact-SQL)](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)   
 [系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
