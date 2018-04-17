---
title: sp_db_vardecimal_storage_format (Transact SQL) |Microsoft 文档
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
- sp_db_vardecimal_storage_format
- sp_db_vardecimal_storage_format_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_vardecimal_storage_format
- decimal data type, compressing
- compressing decimal data
- numeric data type, compressing
- database compression [SQL Server]
- table compression [SQL Server]
ms.assetid: 9920b2f7-b802-4003-913c-978c17ae4542
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7927cee824ca1e3fe4e06283d6aa94cb2d0fce0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spdbvardecimalstorageformat-transact-sql"></a>sp_db_vardecimal_storage_format (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回数据库的当前 vardecimal 存储格式状态，或为数据库启用 vardecimal 存储格式。  从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，始终启用用户数据库。 只有在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中才有必要为数据库启用 vardecimal 存储格式。  
  
> [!IMPORTANT]  
>  更改数据库的 vardecimal 存储格式状态可能会影响备份和恢复、数据库镜像、sp_attach_db、日志传送以及复制。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_db_vardecimal_storage_format [ [ @dbname = ] 'database_name']   
    [ , [ @vardecimal_storage_format = ] { 'ON' | 'OFF' } ]   
[;]  
```  
  
## <a name="arguments"></a>参数  
 [ @dbname=] '*database_name*  
 要更改其存储格式的数据库的名称。 *database_name*是**sysname**，无默认值。 如果省略数据库名称，则返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中所有数据库的 vardecimal 存储格式状态。  
  
 [ @vardecimal_storage_format=] {ON |关闭}  
 指定是否启用 vardecimal 存储格式。 @vardecimal_storage_format 可以是 ON 或 OFF。 该参数是**varchar(3)**，无默认值。 如果提供数据库名称但却省略 @vardecimal_storage_format，则返回指定数据库的当前设置。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，此参数不起作用。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 如果无法更改数据库存储格式，则 sp_db_vardecimal_storage_format 返回错误。 如果数据库已处于指定的状态，则此存储过程无效。  
  
 如果@vardecimal_storage_format不提供参数，将返回数据库名称和 Vardecimal 状态的列。  
  
## <a name="remarks"></a>注释  
 sp_db_vardecimal_storage_format 将返回 vardecimal 状态，但不能更改 vardecimal 状态。  
  
 在以下情况下，sp_db_vardecimal_storage_format 将失败：  
  
-   数据库中有活动用户。  
  
-   已启用数据库进行镜像。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本不支持 vardecimal 存储格式。  
  
 若要将 vardecimal 存储格式状态更改为 OFF，必须将数据库设置为简单恢复模式。 将数据库设置为简单恢复模式时，日志链将断开。 在将 vardecimal 存储格式状态设置为 OFF 后，请执行完整数据库备份。  
  
 如果有表使用 vardecimal 数据库压缩，则将 vardecimal 存储格式状态更改为 OFF 的操作将失败。 若要更改表的存储格式，使用[sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)。 若要确定数据库中有哪些表使用 vardecimal 存储格式，请使用 `OBJECTPROPERTY` 函数并搜索 `TableHasVarDecimalStorageFormat` 属性，如以下示例所示。  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT name, object_id, type_desc  
FROM sys.objects   
 WHERE OBJECTPROPERTY(object_id,   
   N'TableHasVarDecimalStorageFormat') = 1 ;  
GO  
```  
  
## <a name="examples"></a>示例  
 下面的代码在 `AdventureWorks2012` 数据库中启用压缩，确认状态，然后压缩 `Sales.SalesOrderDetail` 表中的 decimal 和 numeric 列。  
  
```  
USE master ;  
GO  
  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON' ;  
GO  
  
-- Check the vardecimal storage format state for  
-- all databases in the instance.  
EXEC sp_db_vardecimal_storage_format ;  
GO  
  
USE AdventureWorks2012 ;  
GO  
  
EXEC sp_tableoption 'Sales.SalesOrderDetail', 'vardecimal storage format', 1 ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
