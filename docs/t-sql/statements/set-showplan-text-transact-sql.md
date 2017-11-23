---
title: "集 SHOWPLAN_TEXT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHOWPLAN_TEXT
- SET_SHOWPLAN_TEXT_TSQL
- SET SHOWPLAN_TEXT
- SHOWPLAN_TEXT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_TEXT statement
- canceling statement execution
- SHOWPLAN_TEXT option
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: 2c4f3fc8-ff2c-4790-8b74-e7e8ef58f9a6
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e0fd12594c0b2a4c5df3a616aeaa48746f781977
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="set-showplantext-transact-sql"></a>SET SHOWPLAN_TEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 而是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回有关如何执行语句的详细信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET SHOWPLAN_TEXT { ON | OFF }  
```  
  
## <a name="remarks"></a>注释  
 SET SHOWPLAN_TEXT 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
 当 SET SHOWPLAN_TEXT 为 ON 时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回每个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的执行信息，但不执行语句。 将该选项设置为 ON 以后，将返回有关所有后续 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句的执行计划信息，直到将该选项设置为 OFF 为止。 例如，如果在 SET SHOWPLAN_TEXT 为 ON 时执行 CREATE TABLE 语句，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将从涉及同一个表的后续 SELECT 语句返回错误信息，以便通知用户：指定的表不存在。 因此，对此表的后续引用将失败。 如果 SET SHOWPLAN_TEXT 是 OFF，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将执行语句，但不生成包含执行计划信息的报表。  
  
 设置 set SHOWPLAN_TEXT 旨在返回 Microsoft Win32 命令提示符下应用程序的可读的输出，例如**osql**实用程序。 SET SHOWPLAN_ALL 则返回更详细的输出，以使专门处理其输出的程序进行处理。  
  
 不能在存储过程中指定 SET SHOWPLAN_TEXT 和 SET SHOWPLAN_ALL。 它们必须是批处理中的唯一语句。  
  
 SET SHOWPLAN_TEXT 将信息作为行集返回，行集形成一个层次结构树，用以表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询处理器在执行每条语句时所采取的步骤。 在输出中，每个语句都有一行说明语句的文本，后面紧接着几行介绍执行步骤的详细信息。 下表显示输出中包含的列。  
  
|列名|Description|  
|-----------------|-----------------|  
|**StmtText**|对于不是 PLAN_ROW 类型的行，该列包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的文本。 对于 PLAN_ROW 类型的行，此列包含对操作的说明。 此列包含物理运算符，也可以选择包含逻辑运算符。 该列的后面还可以跟有由物理运算符决定的说明。 有关物理运算符的详细信息，请参阅**参数**中的列[SET SHOWPLAN_ALL &#40;Transact SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md).|  
  
 有关可以在显示计划输出中看到这些物理和逻辑运算符的详细信息，请参阅[Showplan 逻辑和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)  
  
## <a name="permissions"></a>Permissions  
 为了使用 SET SHOWPLAN_TEXT，你必须具有足够的权限执行执行 SET SHOWPLAN_TEXT 语句，并且必须具有包含引用的对象的所有数据库的 SHOWPLAN 权限。  
  
 为 SELECT、 INSERT、 UPDATE、 DELETE、 EXEC *stored_procedure*，和 EXEC *user_defined_function*语句，以便生成的 Showplan 用户必须：  
  
-   具有执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的相应权限。  
  
-   对包含 Transact-SQL 语句所引用的对象（如表、视图等）的所有数据库拥有 SHOWPLAN 权限。  
  
 对于所有其他语句，如 DDL，使用*database_name*，组、 DECLARE、 动态 SQL 和等等，仅执行的适当权限[!INCLUDE[tsql](../../includes/tsql-md.md)]需要语句。  
  
## <a name="examples"></a>示例  
 此例显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在处理语句时如何使用索引。  
  
 下面是使用索引的查询：  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 下面是结果集：  
  
```  
StmtText                                             
---------------------------------------------------  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;   
  
StmtText                                                                                                                                                                                        
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Seek(OBJECT:([AdventureWorks2012].[Production].[Product].[PK_Product_ProductID]), SEEK:([AdventureWorks2012].[Production].[Product].[ProductID]=CONVERT_IMPLICIT(int,[@1],0)) ORDERED FORWARD)   
```  
  
 下面是不使用索引的查询：  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 下面是结果集：  
  
```  
StmtText                                                                  
------------------------------------------------------------------------  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;   
  
StmtText                                                                                                                                                                                                  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Scan(OBJECT:([AdventureWorks2012].[Production].[ProductCostHistory].[PK_ProductCostHistory_ProductCostID]), WHERE:([AdventureWorks2012].[Production].[ProductCostHistory].[StandardCost]<[@1]))  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [设置 SHOWPLAN_ALL &#40;Transact SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)  
  
  
