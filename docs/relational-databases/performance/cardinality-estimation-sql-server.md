---
title: "基数估计 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 10/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6ef57f8467e87b97024fc08b4916ac4f8e7752b
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="cardinality-estimation-sql-server"></a>基数估计 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  
本文将阐释如何评估和选择 SQL 系统的最佳基数估计 (CE) 配置。 大多数系统受益于最新的 CE，因为它最准确。 CE 将预测查询可能返回的行数。 查询优化器使用基数预测来生成最佳查询计划。 通常，CE 越准确，查询计划就越好。  
  
你的应用程序系统可能具有重要的查询，其计划由于新的 CE 而更改为较慢计划。 此类查询可能为以下任一种：  
  
- OLTP 查询，由于该查询运行相当频繁，因此它的多个实例经常同时运行。  
- 在 OLTP 工作期间运行的具有大量聚合函数的 SELECT 查询。  
  
你可以使用技术来识别因新的 CE 而执行变慢的查询。 你也可以选择如何解决此性能问题。  
  
  
## <a name="versions-of-the-ce"></a>CE 的版本  
  
 在 1998 年，CE 的重大更新是 Microsoft SQL Server 7.0 的一部分，其兼容级别为 70。 后续更新随附在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 中，意味着兼容性级别为 120 和 130。 级别 120 和 130 的 CE 更新中引入了非常适用于现代数据仓库工作负荷和 OLTP（联机事务处理）的假设和算法。  
  
 **兼容性级别：** 通过使用以下 [COMPATIBILITY_LEVEL](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)的 Transact-SQL 代码，可以确保数据库位于特定级别。  

```tsql  
SELECT ServerProperty('ProductVersion');  
go  
  
ALTER DATABASE <yourDatabase>  
    SET COMPATIBILITY_LEVEL = 130;  
go  
  
SELECT    d.name, d.compatibility_level  
    FROM  sys.databases AS d  
    WHERE d.name = 'yourDatabase';  
go  
```  
  
 对于在兼容性级别 120 设置的 SQL Server 数据库，激活跟踪标志 9481 将强制系统使用级别 70 的 CE。  
  
 **旧版 CE：** 对于在兼容性级别 130 设置的数据库，通过使用以下有关 [SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 的 TRANSACT-SQL 语句可以激活级别 70 的 CE。
  
```tsql  
ALTER DATABASE
    SCOPED CONFIGURATION  
        SET LEGACY_CARDINALITY_ESTIMATION = ON;  
go  
  
SELECT  name, value  
    FROM  sys.database_scoped_configurations  
    WHERE name = 'LEGACY_CARDINALITY_ESTIMATION';  
```  
  
 **查询存储：**从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 开始，查询存储是用于检查查询性能的一种方便的工具。  在 SQL Server Management Studio (SSMS.exe) 中的**对象资源管理器**的数据库节点下方，当查询存储设为“开”时，将显示“查询存储”节点。  
  
```tsql  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE = ON;  
go  
  
SELECT  
        q.actual_state_desc    AS [actual_state_desc-ofQueryStore],  
        q.desired_state_desc,  
        q.query_capture_mode_desc  
    FROM  
        sys.database_query_store_options  AS q;  
go  
  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE CLEAR;  
```  
  
 提示：我们建议每个月安装 [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx) 的最新版本。  
  
 跟踪 CE 的基数预测的另一种方法是使用名为 **query_optimizer_estimate_cardinality** 的扩展事件。  以下 T-SQL 代码示例在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上运行。 它将 .xel 文件写入 C:\Temp\（尽管可以更改路径）。 在 SSMS 中打开此 .xel 文件时，其详细信息将以用户友好的方式显示。  
  
```tsql  
DROP EVENT SESSION Test_the_CE_qoec_1 ON SERVER;  
go  
  
CREATE EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    ADD EVENT sqlserver.query_optimizer_estimate_cardinality  
    (  
        ACTION (sqlserver.sql_text)  
            WHERE (  
                sql_text LIKE '%yourTable%'  
                and sql_text LIKE '%SUM(%'  
            )  
    )  
    ADD TARGET package0.asynchronous_file_target   
        (SET  
            filename = 'c:\temp\xe_qoec_1.xel',  
            metadatafile = 'c:\temp\xe_qoec_1.xem'  
        );  
go  
  
ALTER EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    STATE = START;  --STOP;  
go  
```  
  
 有关为 Azure SQL 数据库定制的扩展事件的信息，请参阅 [《Extended events in SQL Database》](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)（SQL 数据库中的扩展事件）。  
  
  
## <a name="steps-to-assess-the-ce-version"></a>评估 CE 版本的步骤  
  
 以下步骤用于评估当使用最新 CE 时最重要的查询的执行是否不佳。 其中一些步骤通过运行上一节中提供的代码示例来执行。  
  
1.  打开 SSMS。 确保将  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库设为最高的可用兼容性级别。  
  
2.  执行以下初始步骤：  
  
    1.  打开 SSMS。  
  
    2.  运行 T-SQL 以确保将  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库设为最高的可用兼容性级别。  
  
    3.  确保数据库已关闭其 LEGACY_CARDINALITY_ESTIMATION 配置。  
  
    4.  清除查询存储。 当然，要确保查询存储已打开。  
  
    5.  运行语句： \`SET NoCount OFF;`  
  
3.  运行语句： \`SET STATISTICS XML ON;`  
  
4.  运行重要的查询。  
  
5.  在结果窗格的“消息”选项卡上，记下实际受影响的行数。  
  
6.  在结果窗格的“结果”选项卡上，双击包含 XML 格式的统计信息的单元格。 将显示图形查询计划。  
  
7.  在图形查询计划的第一个框中右键单击，然后单击“属性”。  
  
8.  针对后面的与不同配置的比较，请记下以下属性的值：  
  
    -   **CardinalityEstimationModelVersion**。  
  
    -   **估计的行数**。  
  
    -   **估计的 I/O 成本**，以及一些涉及实际性能而不是行数预测的类似的估计属性。  
  
    -   **逻辑操作**和**物理操作**。 “并行”是一个不错的选择。  
  
    -   **实际执行模式**。 “批处理”是一个不错的选择，优于“行”。  
  
9. 将估计的行数与实际行数进行比较。 CE 的不准确率偏高或偏低 1% 还是 10%？  
  
10. 运行： \`SET STATISTICS XML OFF;`  
  
11. 运行 T-SQL 以便将数据库的兼容性级别降低一个级别（如从 130 到 120）。  
  
12. 重新运行所有非初始步骤。  
  
13. 比较这两次运行的 CE 属性值。  
  
    - 最新 CE 下的不准确率是不是小于较旧 CE 下的不准确率？  
  
14. 最后，比较这两次运行中的各个性能属性值。  
  
    -   在这两个不同的 CE 估计下你的查询是否使用了不同的计划？  
  
    -   在最新 CE 下你的查询是否运行较缓慢？  
  
    -   除非查询在较旧 CE 下运行地更好，并且使用不同的计划，否则几乎可以肯定地想要最新的 CE。  
  
    -   但是，如果在较旧的 CE 下查询使用较快的计划运行，则将考虑强制系统使用较快计划而忽略 CE。 这种方式可以让你在任何情况下拥有最新 CE，同时在一种独特的情况下保持使用较快计划。  
  
## <a name="how-to-activate-the-best-query-plan"></a>如何激活最佳查询计划  
  
假设在使用新 CE 的情况下，针对查询生成了较慢的查询计划。 以下是一些可以用来激活较快计划的方法。  
  
可以将整个数据库的兼容性级别设置为低于最新级别的值。  
  
- 这可以激活较旧的 CE，但是也使所有查询受制于较旧和不太准确的 CE。  
  
- 此外，较旧级别还将失去查询优化器中的优质改进。  
  
可以使用 LEGACY_CARDINALITY_ESTIMATION 使整个数据库使用较旧 CE，同时保留查询优化器中的改进。  
  
最好的控制方式是强制 SQL 系统在测试期间使用通过较旧 CE 生成的计划。 固定首选计划后，可以将整个数据库设置为使用最新兼容性级别和 CE。 该方法将在后面详细说明。  
  
### <a name="how-to-force-a-particular-query-plan"></a>如何强制使用特定的查询计划  
  
查询存储提供了不同方式来强制系统使用特定的查询计划：  
  
- 执行 **sp_query_store_force_plan**。  
  
- 在 SSMS 中，展开“查询存储”节点，右键单击“资源使用排名靠前的节点”，然后单击“查看资源使用排名靠前的节点”。 此时将显示“强制使用计划”和“取消强制使用计划”按钮。  
  
 有关查询存储的详细信息，请参阅[《Monitoring Performance By Using the Query Store》](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)（使用查询存储监控性能）。  
  
  
## <a name="descriptions-of-advance-ce"></a>高级 CE 的说明  
  
本节介绍了从最新版本的 CE 中实施的改进中获益的示例查询。 这是背景信息，不需要你的具体操作。  
  
### <a name="example-a-ce-understands-maximum-value-might-be-higher-than-when-statistics-were-last-gathered"></a>示例 A. CE 认为最大值可能大于最近收集统计信息时的值  
  
如果 OrderAddedDate 的最大值为 2016-04-30，则假设为 OrderTable 收集统计信息的最近日期为 2016-04-30。 兼容性级别为 120（和更高级别）的 CE 认为数据按升序排序的 OrderTable 中的列的值可能大于由统计信息记录的最大值。 这种假设改进了 SQL SELECT 语句的查询计划，如下所示。  
  
```tsql  
SELECT CustomerId, OrderAddedDate  
    FROM OrderTable  
    WHERE OrderAddedDate >= '2016-05-01';  
```  
  
### <a name="example-b-ce-understands-that-filtered-predicates-on-the-same-table-are-often-correlated"></a>示例 B. CE 认为同一个表的筛选谓词通常是相关的  
  
在下面的 SELECT 语句中我们看到 Make 和 Model 的筛选谓词。 我们可以本能地认为当 Make 为“Honda”时，Model 有可能是“Civic”，前提是 Honda 制造了 Civic。  
  
级别 120 的 CE 认为同一表中 Make 和 Model 两个列之间存在相关性。 CE 对于查询将返回多少行进行更准确的估计，并且查询优化器将生成更优的计划。  
  
```tsql  
SELECT Model_Year, Purchase_Price  
    FROM dbo.Cars  
    WHERE  
        Make  = 'Honda'  AND  
        Model = 'Civic';  
```  
  
### <a name="example-c-ce-no-longer-assumes-any-correlation-between-filtered-predicates-from-different-tables"></a>示例 C. CE 不再假设不同表的筛选谓词之间存在任何相关性  
  
对现代工作负荷和实际业务数据的延伸性的新研究表明，从不同表中筛选的谓词通常没有相互关联性。 在下面的查询中，CE 假设 s.type 与 r.date 之间没有相关性。 因此，CE 对于返回的行数有一个偏低的估计值。  
  
```tsql  
SELECT s.ticket, s.customer, r.store  
    FROM  
                   dbo.Sales    AS s  
        CROSS JOIN dbo.Returns  AS r  
    WHERE  
        s.ticket = r.ticket  AND  
        s.type   = 'toy'     AND  
        r.date   = '2016-05-11';  
```  
  
  
## <a name="see-also"></a>另请参阅  
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  


