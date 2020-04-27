---
title: 迁移查询计划 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66f1f8f57dca3ad2edba3f4b63100b2de3ae5659
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779109"
---
# <a name="migrate-query-plans"></a>迁移查询计划
  大多数情况下，将数据库升级到最新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会提高查询性能。 但是，如果您具有已针对性能进行过认真优化的任务关键查询，在升级前最好为每个查询创建一个计划指南，以保留这些查询的查询计划。 如果在升级后，查询优化器为一个或多个查询选择了效率较低的计划，则可以启用这些计划指南并强制查询优化器使用升级前的计划。  
  
 若要在升级前创建计划指南，请按照以下步骤执行操作：  
  
1.  使用[sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)存储过程并在 USE plan 查询提示中指定查询计划，记录每个任务关键查询的当前计划。  
  
2.  验证计划指南是否适用于此查询。  
  
3.  将数据库升级到最新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     计划保留在升级后的数据库中的计划指南中，如果在升级后计划的性能出现退步，则这些计划将用作后备计划。  
  
     建议您在升级后不要启用计划指南，因为由于统计信息进行了更新，您可能会错过新版本中的更好计划或者重新编译所带来的益处。  
  
4.  如果在升级后选择了效率较低的计划，可以激活所有计划指南或部分计划指南以取代新计划。  
  
## <a name="example"></a>示例  
 下面的示例显示如何通过创建计划指南来为查询记录升级前的计划。  
  
### <a name="step-1-collect-the-plan"></a>步骤 1：收集计划  
 计划指南中记录的查询计划必须采用 XML 格式。 可通过以下方式生成 XML 格式的查询计划：  
  
-   [SET SHOWPLAN_XML](/sql/t-sql/statements/set-showplan-xml-transact-sql)  
  
-   [SET STATISTICS XML](/sql/t-sql/statements/set-statistics-xml-transact-sql)  
  
-   查询[sys.databases dm_exec_query_plan](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql)动态管理函数的 query_plan 列。  
  
-   显示[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] [计划](../../relational-databases/event-classes/showplan-xml-event-class.md)xml、显示[计划 xml 统计信息](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)以及[用于查询编译](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)事件类的显示计划 xml。  
  
 下面的示例通过查询动态管理视图收集语句 `SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;` 的查询计划。  
  
```  
USE AdventureWorks;  
GO  
SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%';  
GO  
```  
  
### <a name="step-2-create-the-plan-guide-to-force-the-plan"></a>步骤 2：创建计划指南以强制实施计划  
 在计划指南中使用 XML 格式的查询计划（通过上述任一方法获取），将该查询计划作为字符串文字复制并粘贴在 sp_create_plan_guide 的 OPTION 子句中指定的 USE PLAN 查询提示中。  
  
 在 XML 计划本身中，先将计划中出现的引号 (') 通过第二个引号进行转义，然后再创建计划指南。 例如，对于包含 `WHERE A.varchar = 'This is a string'` 的计划，必须通过将该代码修改为 `WHERE A.varchar = ''This is a string''` 来进行转义。  
  
 下面的示例为步骤 1 中收集的查询计划创建计划指南，并在 `@hints` 参数中插入此查询的 XML 显示计划。 为简洁起见，此示例中仅包括部分显示计划输出。  
  
```  
EXECUTE sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',  
@type = N'SQL',  
@module_or_batch = NULL,  
@params = NULL,  
@hints = N'OPTION(USE PLAN N''<ShowPlanXML xmlns=''''https://schemas.microsoft.com/sqlserver/2004/07/showplan''''   
    Version=''''0.5'''' Build=''''9.00.1116''''>  
    <BatchSequence><Batch><Statements><StmtSimple>  
    ...  
    </StmtSimple></Statements></Batch>  
    </BatchSequence></ShowPlanXML>'')';  
GO  
```  
  
### <a name="step-3-verify-that-the-plan-guide-is-applied-to-the-query"></a>步骤 3：验证计划指南是否适用于查询  
 再次运行查询，并检查生成的查询计划。 您应看到该计划与您在计划指南中指定的计划相符。  
  
## <a name="see-also"></a>另请参阅  
 [sp_create_plan_guide &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Transact-sql&#41;的查询提示 &#40;](/sql/t-sql/queries/hints-transact-sql-query)   
 [计划指南](../../relational-databases/performance/plan-guides.md)  
  
  
