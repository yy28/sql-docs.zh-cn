---
title: "设置统计信息时间 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_TIME_TSQL
- SET STATISTICS TIME
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- time [SQL Server], statement processing statistics
- SET STATISTICS TIME statement
- STATISTICS TIME option
- statements [SQL Server], statistical information
- parsing [SQL Server], SET STATISTICS TIME statement
- compile times [SQL Server]
- execution processing time [SQL Server]
ms.assetid: eec2e1cd-a29d-4cf3-a271-be9d61506f15
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 523227164984cdabcb65afa3b9213c1cb0d0f18e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="set-statistics-time-transact-sql"></a>SET STATISTICS TIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  显示分析、编译和执行各语句所需的毫秒数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET STATISTICS TIME { ON | OFF }  
```  
  
## <a name="remarks"></a>注释  
 当 SET STATISTICS TIME 为 ON 时，会显示语句的时间统计信息。 为 OFF 时，不显示时间统计信息。  
  
 SET STATISTICS TIME 的设置是在执行或运行时设置，而不是在分析时设置。  
  
 Microsoft[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]无法提供精确的统计信息在纤程模式下，当你启用激活**轻型池**配置选项。  
  
 **Cpu**中的列**sysprocesses**查询执行使用 SET STATISTICS TIME ON 时，才会更新表。 OFF，SET STATISTICS TIME 时**0**返回。  
  
 ON 和 OFF 设置还影响 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 内的“当前活动的进程信息视图”中的 CPU 列。  
  
## <a name="permissions"></a>Permissions  
 若要使用 SET STATISTICS TIME，用户必须具有执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的相应权限。 但不需要 SHOWPLAN 权限。  
  
## <a name="examples"></a>示例  
 下面的示例显示服务器的执行、分析和编译时间。  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS TIME ON;  
GO  
SELECT ProductID, StartDate, EndDate, StandardCost   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS TIME OFF;  
GO  
```  
  
 下面是结果集：  
  
```  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
(269 row(s) affected)  
  
SQL Server Execution Times:  
   CPU time = 0 ms,  elapsed time = 2 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [设置 STATISTICS IO &#40;Transact SQL &#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
