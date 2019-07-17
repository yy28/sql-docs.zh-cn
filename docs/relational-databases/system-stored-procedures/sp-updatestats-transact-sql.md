---
title: sp_updatestats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c00bdd453bc4d1bf467b37aca3639eb43f55e022
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085794"
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

运行`UPDATE STATISTICS`针对当前数据库中的所有用户和内部表。  
  
有关详细信息`UPDATE STATISTICS`，请参阅[UPDATE STATISTICS &#40;TRANSACT-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)。 有关统计信息的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
    
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="arguments"></a>参数  
`[ @resample = ] 'resample'` 指定的**sp_updatestats**将使用的 RESAMPLE 选项[UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)语句。 如果 **'resample'** 未指定，则**sp_updatestats**通过使用默认采样来更新统计信息。 **对重新抽样**是**varchar(8)** 默认值为 no。  
  
## <a name="remarks"></a>备注  
 **sp_updatestats**执行`UPDATE STATISTICS`，通过指定`ALL`关键字，所有用户定义表和内部表在数据库中。 sp_updatestats 将显示指示其进度的消息。 完成更新之后，此存储过程将报告已为所有的表更新了统计信息。  
  
sp_updatestats 更新已禁用非聚集索引的统计信息，但不更新已禁用聚集索引的统计信息。  
  
对于基于磁盘的表， **sp_updatestats**更新统计信息基于**modification_counter**中的信息**sys.dm_db_stats_properties**目录视图，更新统计信息在至少一个该行已被修改。 执行时，将始终更新内存优化表的统计信息**sp_updatestats**。 因此不会执行**sp_updatestats**只在必要时。  
  
**sp_updatestats**可以触发重新编译的存储的过程或其他已编译的代码。 但是， **sp_updatestats**可能不会导致重新编译，如果只有一个查询计划可能引用的表和索引进行。 在这些情况下，即便更新了统计信息也不必进行重新编译。  
  
对于兼容性级别低于 90，执行的数据库**sp_updatestats**不会保留的最新的 NORECOMPUTE 设置为特定的统计信息。 对于兼容性级别为 90 或更高版本的数据库，sp_updatestats 会保留为特定的统计信息最新的 NORECOMPUTE 选项。 有关禁用和重新启用统计信息更新的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定服务器角色或数据库的所有权 (**dbo**)。  

## <a name="examples"></a>示例  
以下示例更新 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中各表的统计信息。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>自动索引和统计信息管理
利用[自适应索引碎片整理](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)等解决方案，自动管理一个或多个数据库的索引碎片整理和统计信息更新。 此过程根据碎片级别以及其他参数，自动选择是重新生成索引还是重新组织索引，并使用线性阈值更新统计信息。

## <a name="see-also"></a>请参阅  
 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS (Transact-SQL)](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)   
 [系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
