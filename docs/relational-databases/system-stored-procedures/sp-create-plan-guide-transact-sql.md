---
title: "sp_create_plan_guide (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide
- sp_create_plan_guide_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_create_plan_guide
ms.assetid: 5a8c8040-4f96-4c74-93ab-15bdefd132f0
caps.latest.revision: "82"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70caae94a352f014757bd00099b43019c08f4a2c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spcreateplanguide-transact-sql"></a>sp_create_plan_guide (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建用于将查询提示或实际查询计划与数据库中的查询关联的计划指南。 有关计划指南的详细信息，请参阅 [Plan Guides](../../relational-databases/performance/plan-guides.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_create_plan_guide [ @name = ] N'plan_guide_name'  
    , [ @stmt = ] N'statement_text'  
    , [ @type = ] N'{ OBJECT | SQL | TEMPLATE }'  
    , [ @module_or_batch = ]  
      {   
                    N'[ schema_name. ] object_name'  
        | N'batch_text'  
        | NULL  
      }  
    , [ @params = ] { N'@parameter_name data_type [ ,...n ]' | NULL }   
    , [ @hints = ] { N'OPTION ( query_hint [ ,...n ] )'   
                 | N'XML_showplan'  
                 | NULL }  
```  
  
## <a name="arguments"></a>参数  
 [ @name =] N*plan_guide_name*  
 是计划指南的名称。 计划指南名称的作用域限于当前数据库。 *plan_guide_name*必须遵从的规则[标识符](../../relational-databases/databases/database-identifiers.md)和不能以数字符号开头 （#）。 最大长度*plan_guide_name*为 124 个字符。  
  
 [ @stmt =] N*statement_text*  
 根据其创建计划指南的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查询优化器识别匹配的查询*statement_text*， *plan_guide_name*将生效。 创建计划指南来成功， *statement_text*必须出现在由指定的上下文@type， @module_or_batch，和@params参数。  
  
 *statement_text*必须允许查询优化器将其与批处理中提供的相应语句或模块由标识匹配的方式提供@module_or_batch和@params。 有关详细信息，请参阅"备注"部分。 大小*statement_text*仅受可用内存的服务器。  
  
 [@type =] N'{对象 |SQL |模板}  
 是实体在其中一种*statement_text*显示。 这将指定匹配的上下文*statement_text*到*plan_guide_name*。  
  
 OBJECT  
 指示*statement_text*的上下文中出现[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程、 标量函数、 多语句表值函数，或[!INCLUDE[tsql](../../includes/tsql-md.md)]当前数据库中的 DML 触发器。  
  
 SQL  
 指示*statement_text*出现在独立的语句或批处理可以提交到上下文中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过任何机制。 [!INCLUDE[tsql](../../includes/tsql-md.md)]提交通过公共语言运行时 (CLR) 对象或扩展存储的过程，或者使用 EXEC N 语句*sql_string*，作为批次在服务器上处理，并因此，应标识为@type  **=**  'SQL'。 如果指定 SQL，则查询提示参数化 {FORCED |不能指定简单}@hints参数。  
  
 TEMPLATE  
 指示计划指南适用于任何查询都会向窗体中所示对参数化*statement_text*。 如果指定模板，则只参数化 {FORCED |简单} 查询提示可以指定在@hints参数。 TEMPLATE 计划指南的详细信息，请参阅[通过使用计划指南指定查询参数化行为](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)。  
  
 [@module_or_batch =] {N'[ *schema_name*。 ] *object_name*|N*batch_text*|NULL}  
 在其中指定的对象名称*statement_text*出现，或在其中的批处理文本*statement_text*显示。 批处理文本不能包括使用*数据库*语句。  
  
 计划指南，以匹配应用程序，从提交一批*batch_tex*t 必须提供相同的格式字符对字符，如提交给[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不会执行内部转换来帮助完成该匹配。 有关详细信息，请参见“备注”部分。  
  
 [*schema_name*。]*object_name*指定的名称[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程、 标量函数、 多语句表值函数，或[!INCLUDE[tsql](../../includes/tsql-md.md)]包含的 DML 触发器*statement_text*. 如果*schema_name*未指定， *schema_name*使用当前用户的架构。 如果指定 NULL 和@type= 'SQL' 的值@module_or_batch设置的值为@stmt。如果@type= 模板，@module_or_batch必须为 NULL。  
  
 [ @params =] {N' *@parameter_name data_type* [，*...n* ] |NULL}  
 指定的定义中嵌入的所有参数*statement_text*。 @params适用以下方法之一时才 true:  
  
-   @type= 'SQL' 或 'TEMPLATE'。 如果 'TEMPLATE'@params必须不为 NULL。  
  
-   *statement_text*通过使用 sp_executesql 和的值提交@params指定参数，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部提交后它中参数化语句。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]来说，从数据库 API（包括 ODBC、OLE DB 和 ADO.NET）提交参数化查询类似于调用 sp_executesql 或 API 服务器游标例程；因此，它们也可以通过 SQL 或 TEMPLATE 计划指南进行匹配。  
  
 *@parameter_namedata_type*作为提交给必须完全相同的格式提供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过使用 sp_executesql 或参数化之后内部提交。 有关详细信息，请参见“备注”部分。 如果批处理不包含参数，则必须指定 NULL。 大小@params仅受可用的服务器内存限制。  
  
 [@hints =] {N'OPTION (*query_hint* [，*...n* ]) |N*XML_showplan*|NULL}  
 N'OPTION (*query_hint* [，*...n* ])  
 指定要附加到匹配的查询的 OPTION 子句@stmt。@hints必须语法上与 SELECT 语句中的 OPTION 子句相同，并且可以包含任何有效查询提示的序列。  
  
 N*XML_showplan*  
 要作为提示应用的、采用 XML 格式的查询计划。  
  
 建议将 XML 显示计划分配给变量；否则，必须通过在单引号前面再加上一个单引号来对显示计划中的任何单引号进行转义。 请参见示例 E。  
  
 NULL  
 指示查询的 OPTION 子句中指定的任何现有提示不应用于该查询。 有关详细信息，请参阅[OPTION 子句 &#40;Transact SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
## <a name="remarks"></a>注释  
 sp_create_plan_guide 的参数必须以显示的顺序提供。 为 **sp_create_plan_guide**的参数提供值时，必须显式指定所有的参数名称，或全部都不指定。 例如，如果指定了 **@name =**，则也必须指定 **@stmt =**、**@type =** 等。 同样，如果省略了 **@name =** 并仅提供了参数值，则其余的参数名称也必须省略并仅提供它们的值。 参数名称仅用于说明，以帮助了解语法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会验证指定的参数名称是否与使用此名称的位置中的参数名称相匹配。  
  
 您可以为相同的查询和批处理或模块创建多个 OBJECT 或 SQL 计划指南。 但是，在任何给定的时间只能启用一个计划指南。  
  
 无法为引用存储过程、函数或 DML 触发器（指定了 WITH ENCRYPTION 子句或为临时触发器）的 @module_or_batch 值创建 OBJECT 类型的计划指南。  
  
 如果尝试删除或修改的函数、存储过程或 DML 触发器由某个计划指南引用，则不管该指南为启用状态还是禁用状态，都会导致错误。 尝试删除计划指南被引用并已为其定义触发器的表也将导致错误。  
  
> [!NOTE]  
>  计划指南不适用于每个 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。 计划指南在任何版本中可见。 包含计划指南的数据库可以附加到任何版本。 将数据库还原或附加到升级版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]后，计划指南保持不变。 执行服务器升级后，应验证每个数据库中计划指南的性能。  
  
## <a name="plan-guide-matching-requirements"></a>符合要求的计划指南  
 指定的计划指南@type= 'SQL' 或@type= 'TEMPLATE' 若要成功匹配的值的查询*batch_text*和 *@parameter_name data_type* [，*...n* ] 必须与应用程序提交它们对应项相同的格式提供。 这表示必须完全按照 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 编译器接收批处理文本的方式来提供批处理文本。 若要捕获实际的批处理和参数文本，可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。 有关详细信息，请参阅[使用 SQL Server 事件探查器的创建和测试计划指南](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)。  
  
 当 @type = 'SQL' 且 @module_or_batch 设置为 NULL 时，则将 @module_or_batch 的值设置为 @stmt 的值。这意味着，值*statement_text*必须完全相同的格式，提供字符对字符，如提交给[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不会执行内部转换来帮助完成该匹配。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匹配的值*statement_text*到*batch_text*和 *@parameter_name data_type* [，*...n* ]，或如果@type= 对象，在相应的查询的文本*object_name*，以下字符串元素不被视为：  
  
-   字符串内部的空白字符（制表符、空格、回车符或换行符）。  
  
-   注释 ( **--** 或 **/ \* \* /** )。  
  
-   尾随分号  
  
 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以匹配*statement_text*字符串`N'SELECT * FROM T WHERE a = 10'`到以下*batch_text*:  
  
 `N'SELECT *`  
  
 `FROM T`  
  
 `WHERE a=10'`  
  
 但是，相同的字符串将不匹配至此*batch_text*:  
  
 `N'SELECT * FROM T WHERE b = 10'`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将忽略第一个查询内部的回车符、换行符和空格字符。 在第二个查询中，序列 `WHERE b = 10` 的解释方式不同于 `WHERE a = 10`。 除了在关键字情况（不区分大小写）中以外，匹配是区分大小写和区分重音的（即使数据库的排序规则不区分大小写）。 对于缩短形式的关键字，匹配不进行区分。 例如，关键字 `EXECUTE`、`EXEC` 和 `execute` 被看作是等价的。  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>计划指南对计划缓存的影响  
 对模块创建计划指南将会从计划缓存中删除该模块的查询计划。 对批处理创建类型为 OBJECT 或 SQL 的计划指南会删除具有相同哈希值的批处理的查询计划。 创建类型为 TEMPLATE 的计划指南会从该数据库中的计划缓存中删除所有单语句批处理。  
  
## <a name="permissions"></a>Permissions  
 若要创建类型为 OBJECT 的计划指南，需要拥有对被引用对象的 ALTER 权限。 若要创建类型为 SQL 或 TEMPLATE 的计划指南，需要拥有对当前数据库的 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-plan-guide-of-type-object-for-a-query-in-a-stored-procedure"></a>A. 为存储过程中的查询创建类型为 OBJECT 的计划指南  
 以下示例创建一个计划指南，它与在基于应用程序的存储过程的上下文中所执行的查询匹配，并将 `OPTIMIZE FOR` 提示应用于该查询。  
  
 下面是此存储过程：  
  
```  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t   
        ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country_region;  
END  
GO  
```  
  
 下面是为此存储过程中的查询所创建的计划指南：  
  
```  
EXEC sp_create_plan_guide   
    @name =  N'Guide1',  
    @stmt = N'SELECT *  
              FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.Customer AS c   
                 ON h.CustomerID = c.CustomerID  
              INNER JOIN Sales.SalesTerritory AS t   
                 ON c.TerritoryID = t.TerritoryID  
              WHERE t.CountryRegionCode = @Country_region',  
    @type = N'OBJECT',  
    @module_or_batch = N'Sales.GetSalesOrderByCountry',  
    @params = NULL,  
    @hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
### <a name="b-creating-a-plan-guide-of-type-sql-for-a-stand-alone-query"></a>B. 为独立查询创建类型为 SQL 的计划指南  
 以下示例创建一个计划指南，它与使用 sp_executesql 系统存储过程的应用程序所提交的批处理中的查询匹配。  
  
 下面是这个批处理：  
  
```  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 若要防止为该查询生成并行执行计划，请创建以下计划指南：  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT TOP 1 *   
              FROM Sales.SalesOrderHeader   
              ORDER BY OrderDate DESC',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (MAXDOP 1)';  
```  
  
### <a name="c-creating-a-plan-guide-of-type-template-for-the-parameterized-form-of-a-query"></a>C. 为参数化格式的查询创建类型为 TEMPLATE 的计划指南  
 以下示例创建一个计划指南，它与被参数化为指定格式的任何查询匹配，并使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 强制执行查询参数化。 下列两个查询在语法上是等价的，差别只是它们的常量文字值。  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 下面是参数化格式的查询的计划指南：  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 在上一个示例中， `@stmt` 参数的值是参数化格式的查询。 获取此值以在 sp_create_plan_guide 中使用的唯一可靠方法是使用 [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) 系统存储过程。 以下脚本既可用来获得参数化查询，又可用来为它创建计划指南。  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  传递到 sp_get_query_template 的 `@stmt`参数中的常量文字值可能会影响为替换该文字的参数选择的数据类型。 这将影响计划指南的匹配。 可能必须创建多个计划指南，以处理不同的参数值范围。  
  
### <a name="d-creating-a-plan-guide-on-a-query-submitted-by-using-an-api-cursor-request"></a>D. 为通过使用 API 游标请求所提交的查询创建计划指南  
 计划指南可以与通过 API 服务器游标例程所提交的查询匹配。 这些例程包括 sp_cursorprepare、sp_cursorprepexec 和 sp_cursoropen。 使用 ADO、OLE DB 和 ODBC API 的应用程序将使用 API 服务器游标与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 频繁交互。 通过查看 RPC:Starting 事件探查器跟踪事件，可以在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 跟踪中看到对 API 服务器游标例程的调用。  
  
 假设以下数据出现在希望用计划指南进行优化的查询的 RPC:Starting 事件探查器跟踪事件中：  
  
```  
DECLARE @p1 int;  
SET @p1=-1;  
DECLARE @p2 int;  
SET @p2=0;  
DECLARE @p5 int;  
SET @p5=4104;  
DECLARE @p6 int;  
SET @p6=8193;  
DECLARE @p7 int;  
SET @p7=0;  
EXEC sp_cursorprepexec @p1 output,@p2 output,N'@P1 varchar(255),@P2 varchar(255)',N'SELECT * FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID WHERE h.OrderDate BETWEEN @P1 AND @P2',@p5 OUTPUT,@p6 OUTPUT,@p7 OUTPUT,'20040101','20050101'  
SELECT @p1, @p2, @p5, @p6, @p7;  
```  
  
 您会注意到，在 `SELECT` 调用中，`sp_cursorprepexec` 查询计划正在使用合并联接，但您希望使用哈希联接。 使用 `sp_cursorprepexec` 所提交的查询将被参数化，包括查询字符串和参数字符串。 您可以完全按照查询字符串和参数字符串在 `sp_cursorprepexec` 调用中的显示方式（字符对字符）来使用它们创建以下计划指南，从而更改对计划的选择。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'APICursorGuide',  
    @stmt = N'SELECT * FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.SalesOrderDetail AS d   
                ON h.SalesOrderID = d.SalesOrderID   
              WHERE h.OrderDate BETWEEN @P1 AND @P2',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = N'@P1 varchar(255),@P2 varchar(255)',  
    @hints = N'OPTION(HASH JOIN)';  
```  
  
 该计划指南将影响应用程序随后对该查询的执行，并且哈希联接将用来处理该查询。  
  
### <a name="e-creating-a-plan-guide-by-obtaining-the-xml-showplan-from-a-cached-plan"></a>E. 通过从缓存计划中获取 XML 显示计划来创建计划指南  
 下面的示例为简单的临时 SQL 语句创建一个计划指南。 在计划指南中，直接在 `@hints` 参数中为查询指定 XML 显示计划，从而为该语句提供了所需的查询计划。 该示例首先通过执行 SQL 语句在计划缓存中生成一个计划。 对于此示例，假定所生成的计划就是所需的计划，不需要做进一步的查询优化。 此查询的 XML 显示计划可通过查询 `sys.dm_exec_query_stats`、 `sys.dm_exec_sql_text`和 `sys.dm_exec_text_query_plan` 动态管理视图获得，并可以分配给 `@xml_showplan` 变量。 然后，将 `@xml_showplan` 变量传递给 `sp_create_plan_guide` 语句中的 `@hints` 参数。 也可以使用 [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) 存储过程从计划缓存中的查询计划中创建计划指南。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints =@xml_showplan;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [计划指南](../../relational-databases/performance/plan-guides.md)   
 [sp_control_plan_guide (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides (Transact-SQL)](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_cached_plans (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sys.fn_validate_plan_guide (Transact-SQL)](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)   
 [sp_get_query_template &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md)  
  
  
