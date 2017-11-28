---
title: "集 SHOWPLAN_XML (Transact SQL) |Microsoft 文档"
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
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs: TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
caps.latest.revision: "48"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2b51e19f70b0ff2119cfe3f89404fe61accf4656
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="set-showplanxml-transact-sql"></a>SET SHOWPLAN_XML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回有关如何以定义好的 XML 文档格式执行上述语句的详细信息。  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET SHOWPLAN_XML { ON | OFF }  
```  
  
## <a name="remarks"></a>注释  
 SET SHOWPLAN_XML 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
 当 SET SHOWPLAN_XML 为 ON，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]无需执行它，返回为每个语句的执行计划信息和[!INCLUDE[tsql](../../includes/tsql-md.md)]不执行语句。 将该选项设置为 ON 以后，将返回有关所有后续 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的执行计划信息，直到将该选项设置为 OFF 为止。 例如，如果在 SET SHOWPLAN_XML 为 ON 时执行 CREATE TABLE 语句，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将从涉及同一个表的后续 SELECT 语句返回错误信息：指定的表不存在。 因此，对此表的后续引用将失败。 如果 SET SHOWPLAN_XML 为 OFF，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将执行语句，但不生成报表。  
  
 SET SHOWPLAN_XML 旨在返回作为输出**nvarchar (max)**为应用程序，如**sqlcmd**实用程序，其中的 XML 输出随后由其他工具来显示和处理查询计划信息。  
  
> [!NOTE]  
>  动态管理视图中， **sys.dm_exec_query_plan**，返回与相同的信息在 SET SHOWPLAN XML **xml**数据类型。 此信息返回从**query_plan**列**sys.dm_exec_query_plan**。 有关详细信息，请参阅[sys.dm_exec_query_plan &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
 不能在存储过程内部指定 SET SHOWPLAN_XML。 该语句必须是批处理中的唯一语句。  
  
 SET SHOWPLAN_XML 将返回一组 XML 文档信息。 SET SHOWPLAN_XML ON 语句之后的每个批处理都将在单个文档输出中得到反映。 每个文档都包含批处理中语句的文本，后跟执行步骤的详细信息。 该文档可以显示估计的开销、行数、访问的索引数、执行的运算符的类型、联接次序以及有关执行计划的详细信息。  
  
 在安装了 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机的本地目录上安装，将复制包含 XML 架构的文档（该架构用于来自 SET SHOWPLAN_XML 的 XML 输出）。 它可以在包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文件的驱动器上找到，具体位置如下：  
  
 \Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 Showplan 架构也可以位于[此网站](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)。  
  
> [!NOTE]  
>  如果**包括实际的执行计划**中选择[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，则此设置选项不会生成 XML 显示计划输出。 清除**包括实际的执行计划**按钮之前使用此设置选项。  
  
## <a name="permissions"></a>Permissions  
 必须对执行 SET SHOWPLAN_XML 的语句具有足够的执行权限，必须对包含被引用对象的所有数据库具有 SHOWPLAN 权限。  
  
 为 SELECT、 INSERT、 UPDATE、 DELETE、 EXEC *stored_procedure*，和 EXEC *user_defined_function*语句，以便生成的 Showplan 用户必须：  
  
-   具有执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的相应权限。  
  
-   对于包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句引用的对象（如表、视图等）的所有数据库，具有 SHOWPLAN 权限。  
  
 对于所有其他语句，如 DDL，使用*database_name*，组、 DECLARE、 动态 SQL 和等等，仅执行的适当权限[!INCLUDE[tsql](../../includes/tsql-md.md)]需要语句。  
  
## <a name="examples"></a>示例  
 下面两个语句使用了 SET SHOWPLAN_XML 设置，以显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在查询中分析和优化索引的方法。  
  
 第一个查询在 WHERE 子句中使用针对索引列的等于比较运算符 (=)。 第二个查询在 WHERE 子句中使用 LIKE 运算符。 这将强制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要使用聚集的索引扫描和查找满足 WHERE 子句条件的数据。 中的值**EstimateRows**和**EstimatedTotalSubtreeCost**属性是更小，以指示它更快地处理，并使用更少的资源比第一个索引查询索引的查询。  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_XML ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, JobTitle  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Production%';  
GO  
SET SHOWPLAN_XML OFF;  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
