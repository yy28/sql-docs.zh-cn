---
title: PERCENT_RANK (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PERCENT_RANK_TSQL
- PERCENT_RANK
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENT_RANK function
- analytic functions, PERCENT_RANK
ms.assetid: e361c2d4-c01f-4da4-8e89-1ddc724a2629
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f506b8f3007157f9e1757da76442af848d023494
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="percentrank-transact-sql"></a>PERCENT_RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  计算 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中一组行内某行的相对排名。 使用 PERCENT_RANK 计算一个值在查询结果集或分区中的相对位置。 PERCENT_RANK 类似于 CUME_DIST 函数。  
  
## <a name="syntax"></a>语法  
  
```  
PERCENT_RANK( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>参数  
 OVER ( [ partition_by_clause ] order_by_clause)  
 partition_by_clause 将 FROM 子句生成的结果集划分为要应用函数的分区。 如果未指定，则此函数将查询结果集的所有行视为单个组。 order_by_clause 确定执行操作的逻辑顺序。 需要 order_by_clause。 不能在 PERCENT_RANK 函数中指定 OVER 语法的 \<rows 或 range 子句>。  有关详细信息，请参阅 [OVER 子句 (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md)。  
  
## <a name="return-types"></a>返回类型  
 **float(53)**  
  
## <a name="general-remarks"></a>一般备注  
 PERCENT_RANK 返回的值范围大于 0 并小于或等于 1。 任何一组中第一行的 PERCENT_RANK 都为 0。 默认情况下包含 NULL 值，且该值被视为最低的可能值。  
  
 PERCENT_RANK 具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>示例  
 下面的示例使用 CUME_DIST 函数计算给定部门内每个雇员的薪金百分比。 CUME_DIST 函数返回的值表示薪金低于或等于同一个部门中当前雇员的雇员百分比。 PERCENT_RANK 函数将雇员的薪金在部门内的排名计算为一个百分比。 指定 PARTITION BY 子句来按部门对结果集中的行进行分区。 OVER 子句中的 ORDER BY 子句对每个分区中的行进行排序。 SELECT 语句中的 ORDER BY 子句对整个结果集中的行进行排序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate,   
       CUME_DIST () OVER (PARTITION BY Department ORDER BY Rate) AS CumeDist,   
       PERCENT_RANK() OVER (PARTITION BY Department ORDER BY Rate ) AS PctRank  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
    INNER JOIN HumanResources.EmployeePayHistory AS e    
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control')   
ORDER BY Department, Rate DESC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department             LastName               Rate                  CumeDist               PctRank  
---------------------- ---------------------- --------------------- ---------------------- ----------------------  
Document Control       Arifin                 17.7885               1                      1  
Document Control       Norred                 16.8269               0.8                    0.5  
Document Control       Kharatishvili          16.8269               0.8                    0.5  
Document Control       Chai                   10.25                 0.4                    0  
Document Control       Berge                  10.25                 0.4                    0  
Information Services   Trenary                50.4808               1                      1  
Information Services   Conroy                 39.6635               0.9                    0.888888888888889  
Information Services   Ajenstat               38.4615               0.8                    0.666666666666667  
Information Services   Wilson                 38.4615               0.8                    0.666666666666667  
Information Services   Sharma                 32.4519               0.6                    0.444444444444444  
Information Services   Connelly               32.4519               0.6                    0.444444444444444  
Information Services   Berg                   27.4038               0.4                    0  
Information Services   Meyyappan              27.4038               0.4                    0  
Information Services   Bacon                  27.4038               0.4                    0  
Information Services   Bueno                  27.4038               0.4                    0  
(15 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [CUME_DIST (Transact-SQL)](../../t-sql/functions/cume-dist-transact-sql.md)  
  
  
