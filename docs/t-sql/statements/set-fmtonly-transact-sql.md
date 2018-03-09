---
title: "集 FMTONLY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FMTONLY_TSQL
- FMTONLY
- SET FMTONLY
- SET_FMTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], only metadata returned
- SET FMTONLY statement
- FMTONLY option
ms.assetid: 02a1d9ac-2e58-433c-9a07-2c5a4a2214e1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 38625e3079956032513bb0e26c5d37b9a7071fea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="set-fmtonly-transact-sql"></a>SET FMTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  只将元数据返回给客户端。 可以用于测试响应的格式，而不必实际执行查询。  
  
> [!NOTE]  
>  请勿使用此功能。 此功能已被取代[sp_describe_first_result_set &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)， [sp_describe_undeclared_parameters &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)， [sys.dm_exec_describe_first_result_set &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)，和[sys.dm_exec_describe_first_result_set_for_object &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SET FMTONLY { ON | OFF }   
```  
  
## <a name="remarks"></a>注释  
 当 SET FMTONLY 为 ON 时，不会因请求而对任何行进行处理或将其发送到客户端。  
  
 SET FMTONLY 的设置是在执行或运行时设置，而不是在分析时设置。  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>答： 查看而不实际运行查询的查询的列标头信息。  
 以下示例将 `SET FMTONLY` 设置更改为 `ON`，并执行 `SELECT` 语句。 该设置使上述语句只返回列信息，而不返回数据行。  
  
```  
USE AdventureWorks2012;  
GO  
SET FMTONLY ON;  
GO  
SELECT *   
FROM HumanResources.Employee;  
GO  
SET FMTONLY OFF;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>B. 而不实际运行查询查看查询的列标头信息。  
 下面的示例演示如何返回仅列标头 （元数据） 查询的信息。 批处理开头 FMTONLY 设置为 OFF，并在 SELECT 语句之前更改为 ON 的 FMTONLY。 这将导致 SELECT 语句以返回仅列标题;不返回任何数据行。  
  
```  
-- Uses AdventureWorks  
  
BEGIN  
    SET FMTONLY OFF;  
    SET DATEFORMAT mdy;  
    SET FMTONLY ON;  
    SELECT * FROM dbo.DimCustomer;  
    SET FMTONLY OFF;  
END  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

