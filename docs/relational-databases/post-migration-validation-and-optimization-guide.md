---
title: "迁移后验证和优化指南 |Microsoft 文档"
ms.custom: 
ms.date: 5/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: 3
author: pelopes
ms.author: harinid
manager: 
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: d81eabfa1bdb5736bbf6f53ed34c2e1ac157e782
ms.contentlocale: zh-cn
ms.lasthandoff: 05/25/2017

---
# <a name="post-migration-validation-and-optimization-guide"></a>迁移后验证和优化指南
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]post 迁移步骤是非常重要的协调任何数据准确性和完整性，以及发现与工作负荷的性能问题。

# <a name="common-performance-scenarios"></a>常见的性能方案 
以下是一些常见的性能方案在迁移到后遇到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]平台和如何解决这些问题。 其中包括的方案是到 specifdic[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移 （较旧版本中的较新版本），以及外的平台 （例如 Oracle、 DB2、 MySQL 和 Sybase） 到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移。

## <a name="Parameter Sniffing"></a>参数探查的敏感性

**适用于：**外的平台 （例如 Oracle、 DB2、 MySQL 和 Sybase） 到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移。

> [!NOTE]
> 有关[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移，如果此问题已在源中存在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 迁移到较新版本的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]作为-将不满足这种方案。 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]通过使用探查输入数据分布在第一个编译，生成参数化且可重复使用计划，针对进行了优化的输入的参数的存储过程的编译查询计划。 即使不存储过程，生成普通计划的大多数语句将参数化。 第一次缓存某一计划后，任何将来的执行将映射到以前缓存的计划。
当该首次编译可能不具有用于参数的最常见集常用工作负荷时，将出现的潜在问题。 不同的参数相同的执行计划变得效率低下。

### <a name="steps-to-resolve"></a>若要解决的步骤

1.    使用`RECOMPILE`提示。 每次改写，以便为每个参数的值，都会计算计划。
2.    重写存储的过程以使用选项`(OPTIMIZE FOR(<input parameter> = <value>))`。 决定要使用它的值适合大多数相关的工作负荷，创建和维护变得有效的参数化值的一个计划。
3.    重写使用过程中的本地变量的存储的过程。 现在，优化器将用于估计，导致相同的计划而不考虑的参数值的密度向量。
4.    重写存储的过程以使用选项`(OPTIMIZE FOR UNKNOWN)`。 使用本地变量的方法相同的效果。
5.    重写查询以使用提示`DISABLE_PARAMETER_SNIFFING`。 相同效果与使用本地变量技术通过完全禁用参数探查，除非`OPTION(RECOMPILE)`，`WITH RECOMPILE`或`OPTIMIZE FOR <value>`使用。

> [!TIP] 
> 利用[!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]计划分析功能来快速确定这是否是问题。 可用的详细信息[此处](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier/)。

## <a name="Missing indexes"></a>缺失索引

**适用于：**外的平台 （如 Oracle、 DB2、 MySQL 和 Sybase） 和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移。

不正确或缺失索引会导致额外的 I/O 会导致额外的内存和 CPU 要花大量时间。 可能是因为工作负荷配置文件已更改如使用不同谓词，从而导致无效现有索引设计。 证据不佳的索引策略或工作负荷配置文件中的更改包括：
-   查找重复项，冗余，很少使用的和完全未使用的索引。
-   具有与更新的未使用索引的格外小心。

### <a name="steps-to-resolve"></a>若要解决的步骤

1.    利用任何缺少的索引引用的图形执行计划。
2.    索引生成的建议[数据库引擎优化顾问](../tools/dta/tutorial-database-engine-tuning-advisor.md)。
3.    利用[缺失索引 DMV](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)或通过[SQL Server 性能仪表板](https://www.microsoft.com/en-us/download/details.aspx?id=29063)。
4.    利用预先存在可以使用现有的 Dmv 来深入了解任何缺少、 重复、 冗余、 极少使用和完全未使用的索引，但还如果任何索引引用为提示/硬编码到你的数据库中现有的过程和函数的脚本。 

> [!TIP] 
> 此类预先存在的脚本的示例包括[索引创建](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation)和[索引信息](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information)。 

## <a name="Inability to use predicates"></a>无法使用谓词以筛选数据

**适用于：**外的平台 （如 Oracle、 DB2、 MySQL 和 Sybase） 和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移。

> [!NOTE]
> 有关[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移，如果此问题已在源中存在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 迁移到较新版本的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]作为-将不满足这种方案。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]查询优化器可以只相当于在编译时已知的信息。 如果工作负荷依赖于仅可以在执行时已知的谓词，然后不佳的计划选择可能会增加。 好的计划，谓词必须为**可优化**，或**S**earch **Arg**ument**可以**。

非可优化谓词的一些示例：
-   隐式数据转换，如 VARCHAR 为 NVARCHAR 或将整型转换为 VARCHAR。 查找中实际的执行计划的运行时 CONVERT_IMPLICIT 警告。 将从一种类型转换为另一个也会导致精度损失。
-   复杂的不确定性的表达式，如`WHERE UnitPrice + 1 < 3.975`，但不是`WHERE UnitPrice < 320 * 200 * 32`。
-   表达式使用函数，如`WHERE ABS(ProductID) = 771`或`WHERE UPPER(LastName) = 'Smith'`
-   带有前导通配符，如字符串`WHERE LastName LIKE '%Smith'`，但不是`WHERE LastName LIKE 'Smith%'`。

### <a name="steps-to-resolve"></a>若要解决的步骤

1. 始终将变量/参数声明为所需目标[数据类型](../t-sql/data-types/data-types-transact-sql.md)。 
  -   这可能涉及进行比较 （如存储的过程、 用户定义函数或视图） 带有保留在基础表中使用的数据类型的信息的系统表的数据库中存储任何用户定义的代码构造 (如[sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md))。
2. 如果找不到上一个点遍历所有代码，然后为同一目的，更改表上的数据类型，以匹配任何变量/参数声明。
3. 原因出以下构造的用途：
  -   作为谓词; 正在使用的函数
  -   通配符搜索;
  -   基于列式数据 – 的复杂表达式的计算结果需要改为创建持久化计算的列，可编制索引;

> [!NOTE] 
> 上述所有事项，可以进行 programmaticaly。

## <a name="Table Valued Functions"></a>使用表值函数 (多语句 vs 内联)

**适用于：**外的平台 （如 Oracle、 DB2、 MySQL 和 Sybase） 和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移。

> [!NOTE]
> 有关[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移，如果此问题已在源中存在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 迁移到较新版本的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]作为-将不满足这种方案。

表值函数返回的表数据类型可以是视图的替代方法。 限于单个视图时`SELECT`语句中，用户定义函数可以包含允许更多逻辑不能在视图中的其他语句。

> [!IMPORTANT] 
> 由于在编译时，不创建输出表的 MSTVF （多语句表值函数），因此[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]查询优化器依赖于启发式技术，并不是实际统计信息，并确定行估计。 即使索引添加到基表，这不要帮助。 有关 MSTVFs，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 1 的固定的估计的行数应为应该由 MSTVF (开头[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]修复估计是 100 行)。

### <a name="steps-to-resolve"></a>若要解决的步骤
1.    多语句 TVF 是否仅在单个语句，将转换为内联 TVF。

    ```tsql
    CREATE FUNCTION dbo.tfnGetRecentAddress(@ID int)
    RETURNS @tblAddress TABLE
    ([Address] VARCHAR(60) NOT NULL)
    AS
    BEGIN
      INSERT INTO @tblAddress ([Address])
      SELECT TOP 1 [AddressLine1]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    RETURN
    END
    ```
    若要 

    ```tsql
    CREATE FUNCTION dbo.tfnGetRecentAddress_inline(@ID int)
    RETURNS TABLE
    AS
    RETURN (
      SELECT TOP 1 [AddressLine1] AS [Address]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    )
    ```

2.    如果更复杂，请考虑使用存储在内存优化表或临时表中的中间结果。

##  <a name="Additional_Reading"></a> 其他阅读主题  
 [Query Store 最佳实践](../relational-databases/performance/best-practice-with-the-query-store.md)  
[内存优化表](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
[用户定义函数](../relational-databases/user-defined-functions/user-defined-functions.md)  
[表变量和行估计-第 1 部分](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/11/30/table-variables-and-row-estimations-part-1/)  
[表变量和行估计-第 2 部分](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/12/09/table-variables-and-row-estimations-part-2/)  
[执行计划缓存和重用](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)

