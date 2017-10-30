---
title: "DROP PROCEDURE (TRANSACT-SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP PROCEDURE
- DROP_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing stored procedures
- dropping procedure groups
- deleting stored procedures
- deleting procedure groups
- DROP PROCEDURE statement
- dropping stored procedures
- stored procedures [SQL Server], removing
- removing procedure groups
ms.assetid: 1c2d7235-7b9b-4336-8f17-429e7d82c2c3
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b386dfca28622eb95eec500d909aa7190d081493
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的当前数据库中删除一个或多个存储过程或过程组。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 仅当它已存在，则有条件地删除过程。  
  
 *schema_name*  
 该过程所属的架构的名称。 不能指定服务器名称或数据库名称。  
  
 *过程*  
 要删除的存储过程或存储过程组的名称。 编号的过程组中的单独过程不能删除;整个过程组将被丢弃。  
  
## <a name="best-practices"></a>最佳实践  
 在删除任何存储过程之前，请检查依赖对象，并且相应地修改这些对象。 如果没有更新这些对象，则删除存储过程可能会导致依赖对象和脚本失败。 有关详细信息，请参阅[查看存储过程的依赖关系](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
## <a name="metadata"></a>元数据  
 若要显示现有过程的列表，请查询**sys.objects**目录视图。 若要显示过程定义，请查询**sys.sql_modules**目录视图。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要**控件**对该过程的权限或**ALTER**权限过程所属的架构或中的成员身份**db_ddladmin**固定的服务器角色.  
  
## <a name="examples"></a>示例  
 下面的示例将删除当前数据库中的 `dbo.uspMyProc` 存储过程。  
  
```  
DROP PROCEDURE dbo.uspMyProc;  
GO  
```  
  
 下面的示例将删除当前数据库中的多个存储过程。  
  
```  
DROP PROCEDURE dbo.uspGetSalesbyMonth, dbo.uspUpdateSalesQuotes, dbo.uspGetSalesByYear;  
```  
  
 下面的示例删除`dbo.uspMyProc`存储过程，如果它存在，但如果过程不存在不导致错误。 此语法是中的新增功能[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>另请参阅  
 [ALTER PROCEDURE (Transact-SQL)](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [删除存储过程](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  



