---
title: 重大更改数据库引擎 SQL Server 2014 中的功能 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cfb905cb56c053d44b93021838915d3a628241a0
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420202"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2014"></a>SQL Server 2014 中数据库引擎功能的重大更改
  本主题介绍中的重大更改[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]及更早版本的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 这些更改可能导致基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的早期版本的应用程序、脚本或功能无法继续使用。 在进行升级时可能会遇到这些问题。 有关详细信息，请参阅 [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
##  <a name="SQL14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中的重大更改  
 没有新问题。  
  
##  <a name="Denali"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中的重大更改  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|功能|Description|  
|-------------|-----------------|  
|从名为 NEXT 的列或表中进行选择|序列使用 ANSI 标准 NEXT VALUE FOR 函数。 如果表或列名为 NEXT 且表或列的别名为 VALUE，和 ANSI 标准 AS 被省略，则所得到的语句可能导致错误。 若要解决这个问题，请包括 ANSI 标准 AS 关键字。 例如，`SELECT NEXT VALUE FROM Table` 应被重写为 `SELECT NEXT AS VALUE FROM Table`，`SELECT Col1 FROM NEXT VALUE` 应被重写为 `SELECT Col1 FROM NEXT AS VALUE`。|  
|PIVOT 运算符|当数据库兼容性级别设置为 110 时，不允许在递归公用表表达式 (CTE) 查询中使用 PIVOT 运算符。 重写该查询，或将兼容性级别设置为 100 或更低。 当每个分组有多个行时，在递归 CTE 查询中使用 PIVOT 会产生不正确的结果。|  
|sp_setapprole 和 sp_unsetapprole|`OUTPUT` 的 cookie `sp_setapprole` 参数当前记载为 `varbinary(8000)`，这是正确的最大长度。 但是，当前实现返回 `varbinary(50)`。 应用程序应继续保留 `varbinary(8000)`，以便当 cookie 在将来的版本中返回大小增量时，应用程序可继续正确运行。 有关详细信息，请参阅 [sp_setapprole (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql)。|  
|EXECUTE AS|EXECUTE AS 的 cookie OUTPUT 参数当前记载为 `varbinary(8000)`，这是正确的最大长度。 但是，当前实现返回 `varbinary(100)`。 应用程序应继续保留 `varbinary(8000)`，以便当 cookie 在将来的版本中返回大小增量时，应用程序可继续正确运行。 有关详细信息，请参阅 [EXECUTE AS (Transact SQL)](/sql/t-sql/statements/execute-as-transact-sql)。|  
|sys.fn_get_audit_file 函数|两个其他列 (**user_defined_event_id**并**user_defined_information**) 已添加以支持用户定义的审核事件。 不按名称选择列的应用程序可能会返回比预期更多的列。 请按名称选择列，或调整应用程序以接受这些额外的列。|  
|WITHIN 保留关键字|WITHIN 现在是保留关键字。 引用名为“within”的对象或列将失败。 重命名对象或列，或通过使用括号或引号来分隔名称。  例如，`SELECT * FROM [within]`。|  
|对类型为 `time` 或 `datetime2` 的计算列的 CAST 和 CONVERT 操作|在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的早期版本中，对 `time` 或 `datetime2` 数据类型的 CAST 和 CONVERT 操作的默认样式为 121，当在计算列表达式中使用这些类型时除外。 对于计算列，默认样式为 0。 当创建用于涉及自动参数化的查询中或约束定义中的计算列时，此行为会影响计算列。<br /><br /> 兼容性级别为 110 时，对 `time` 和 `datetime2` 数据类型的 CAST 和 CONVERT 操作的默认样式始终为 121。 如果您的查询依赖旧行为，请使用低于 110 的兼容性级别或在受影响的查询中显式指定 0 样式。<br /><br /> 将数据库升级到兼容性级别 110 将不更改已存储到磁盘的用户数据。 您必须相应手动更正此数据。 例如，如果您使用了 SELECT INTO 来从包含上述计算列表达式的源创建表，将存储数据（使用样式 0）而非存储计算列定义本身。 您需要手动更新此数据，以匹配样式 121。|  
|ALTER TABLE|ALTER TABLE 语句只允许两部分的表名称 (schema.object)。 在编译时出现错误 117 失败，指定表名现在使用以下格式：<br /><br /> server.database.schema.table<br /><br /> .database.schema.table<br /><br /> ..schema.table<br /><br /> 在早期版本中指定格式 server.database.schema.table 会返回错误 4902。 指定格式 .database.schema.table 或 ..schema.table 则会成功。 要解决此问题，请不要使用 4 部分的前缀。|  
|浏览元数据|使用 FOR BROWSE 或 SET NO_BROWSETABLE ON 查询视图时，现在会返回视图的元数据而非基础对象的元数据。 此行为现在匹配浏览元数据的其他方法。|  
|SOUNDEX|数据库兼容级别为 110 时，SOUNDEX 函数实现的新规则可能导致由该函数计算的值不同于更低兼容级别时计算的值。 在升级到兼容性级别 110 后，可能需要重新生成使用 SOUNDEX 函数的索引、堆或 CHECK 约束。 有关详细信息，请参阅 [SOUNDEX (Transact-SQL)](/sql/t-sql/functions/soundex-transact-sql)
|失败的 DML 语句的行计数消息|在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，DML 语句失败时，[!INCLUDE[ssDE](../includes/ssde-md.md)] 将以一致方式将包含 RowCount:0 的 TDS DONE 令牌发送到客户端。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的早期版本中，当 TRY-CATCH 块包含失败的 DML 语句并且该语句由[!INCLUDE[ssDE](../includes/ssde-md.md)]自动参数化或 TRY-CATCH 块所处的级别不同于失败语句的级别时，会向客户端发送不正确的值 -1。 例如，如果 TRY-CATCH 块调用存储过程且该过程中的 DML 语句失败，客户端将错误地收到 -1 值。<br /><br /> 依赖这种不正确行为的应用程序将失败。|  
|SERVERPROPERTY (Edition)|所安装的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 实例的产品版本。 使用该属性的值确定已安装的产品支持的功能和限制（如最大 CPU 数）。<br /><br /> 根据安装的 Enterprise 版，此方法可返回 Enterprise Edition 或 Enterprise Edition:基于内核授予许可。 根据单个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的最大计算能力来区分 Enterprise 版本。 有关详细信息中的计算能力限制[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]，请参阅[Compute Capacity Limits by Edition 的 SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。|  
|CREATE LOGIN|`CREATE LOGIN WITH PASSWORD = '`*密码*`' HASHED`选项不能用于创建的哈希[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]7 或更早版本。|  
|`datetimeoffset` 的 CAST 和 CONVERT 转换|在从日期和数据类型转换为 `datetimeoffset` 时，只支持样式 0 或 1。 所有其他转换样式均返回错误 9809。 例如，下面的代码将返回错误 9809。<br /><br /> `SELECT CONVERT(date, CAST('7070-11-25 16:25:01.00986 -02:07' as datetimeoffset(5)), 107);`|  
  
### <a name="dynamic-management-views"></a>动态管理视图  
  
|“查看”|Description|  
|----------|-----------------|  
|sys.dm_exec_requests|该命令列从 `nvarchar(16)` 更改为 `nvarchar(32)`。|  
|sys.dm_os_memory_cache_counters|已重命名以下列：<br /><br /> single_pages_kb 现在是： <br />                          pages_kb<br /><br /> multi_pages_kb<br />                           现在是： pages_in_use_kb|  
|sys.dm_os_memory_cache_entries|列 pages_allocated_count 列已重命名为的 pages_kb。|  
|sys.dm_os_memory_clerks|已删除列 multi_pages_kb。<br /><br /> 列 single_pages_kb 列已重命名为的 pages_kb。|  
|sys.dm_os_memory_nodes|已重命名以下列：<br /><br /> single_pages_kb 现在是： <br />                            pages_kb<br /><br /> multi_pages_kb 现在是： <br />                            foreign_committed_kb|  
|sys.dm_os_memory_objects|以下列已重命名。<br /><br /> pages_allocated_count 现在是：<br />                            pages_in_bytes<br /><br /> max_pages_allocated_count is now: max_pages_in_bytes|  
|sys.dm_os_sys_info|已重命名以下列：<br /><br /> physical_memory_in_bytes 现在是： <br />                            physical_memory_kb<br /><br /> bpool_commit_target 现在是： <br />                            committed_target_kb<br /><br /> 现在，bpool_visible 是： <br />                            visible_target_kb<br /><br /> virtual_memory_in_bytes 现在是： <br />                            virtual_memory_kb<br /><br /> bpool_commited 现在是：<br />                            committed_kb|  
|sys.dm_os_workers|区域设置列已删除。|  
  
### <a name="catalog-views"></a>目录视图  
  
|“查看”|Description|  
|----------|-----------------|  
|sys.data_spaces<br /><br /> sys.partition_schemes<br /><br /> sys.filegroups<br /><br /> sys.partition_functions|已将新列 is_system 添加到 sys.data_spaces 和 sys.partition_functions。 （sys.partition_schemes 和 sys.filegroups 将继承 sys.data_spaces 的列。）<br /><br /> 此列中的值 1 指示该对象用于全文检索片段。<br /><br /> 在 sys.partition_functions、sys.partition_schemes 和 sys.filegroups 中，新列不是最后一列。 请修改依赖于从这些目录视图中返回的列顺序的现有查询。|  
  
### <a name="sql-clr-data-types-geometry-geography-and-hierarchyid"></a>SQL CLR 数据类型（geometry、geography 和 hierarchyid）  
 程序集**Microsoft.SqlServer.Types.dll**，其中包含空间数据类型和 hierarchyid 类型具有已从版本 10.0 升级到版本 11.0。 满足以下条件时，引用此程序集的自定义应用程序可能失败：  
  
-   移动时自定义应用程序从一台计算机依据[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]到仅计算机上安装[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]是安装，该应用程序将失败，因为的被引用的版本 10.0 **SqlTypes**程序集不存在。 你可能会看到以下错误消息：`"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   当引用**SqlTypes**程序集版本 11.0 和也安装了版本 10.0，可能会看到此错误消息： `"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   当引用**SqlTypes**从面向.NET 3.5、 4 或 4.5 的自定义应用程序的程序集版本 11.0，该应用程序将失败，因为 SqlClient 按设计加载的程序集的版本 10.0。 当应用程序调用以下方法之一时，将出现此失败：  
  
    -   `GetValue` 类的 `SqlDataReader` 方法  
  
    -   `GetValues` 类的 `SqlDataReader` 方法  
  
    -   `SqlDataReader` 类的方括号索引运算符 []  
  
    -   `ExecuteScalar` 类的 `SqlCommand` 方法  
  
 您可以使用以下方法之一来解决此问题：  
  
-   您可以通过调用 `GetSqlBytes` 方法替代以上所列的 Get 方法来检索 CLR [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 系统类型，在您的代码中解决此问题，如以下示例中所示：  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   您可以通过在应用程序配置文件中使用程序集重定向来解决此问题，如以下示例中所示：  
  
    ```xml  
    <runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    <runtime>  
    ```  
  
-   您可以通过为“类型系统版本”属性指定值“SQL Server 2012”以强制 SqlClient 加载程序集的版本 11.0，解决此问题。 此连接字符串属性仅在 .NET 4.5 和更高版本中使用。  
  
-   `assemblyBinding` 标记必须包装在 `runtime` 标记下。  
  
### <a name="support-for-awe"></a>对 AWE 的支持  
 32 位地址窗口化扩展插件 (AWE) 已不受支持。 这可能会导致在 32 位操作系统上性能下降。 对于占用大量内存的安装，请迁移到 64 位操作系统。  
  
### <a name="xquery-functions-are-surrogate-aware"></a>XQuery 函数可识别代理项  
 XQuery 函数和运算符的 W3C 建议要求它们对代理项对进行计数，该代理项对用 UTF-16 编码将大范围 Unicode 字符表示单个符号。 但是，在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 版本中，字符串函数不能将代理对识别为单个字符。 某些字符串操作-例如，字符串长度计算和子字符串提取-返回不正确的结果。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 现在完全支持 UTF-16，可正确处理代理项对。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 XML 数据类型只允许格式正确的代理项对。 但在某些情况下，一些函数仍会返回未定义的结果或意外结果，这是因为可能会将无效的或部分代理项对作为字符串值传递给 XQuery 函数。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中使用 XQuery 时，请考虑以下生成字符串值的方法：  
  
-   提供常量字符串值作为二进制值。  在使用此方法时，仍可能传递无效的或部分代理项对。  
  
-   通过提供字符实体来提供常量字符串值。  使用此方法时，仍可能传递无效或不完整代理对。 XQuery 函数需要高级字符的单字符实体。 如果提供代理项对字符的字符实体，这些函数将引发错误。  
  
-   使用导入外部值**sql: column**或**sql: variable**。 在使用这些方法时，仍可能引入无效的或部分代理项对。  
  
#### <a name="affected-xquery-functions-and-operators"></a>受影响的 XQuery 函数和运算符  
 以下 XQuery 函数和运算符现在可在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中正确处理 UTF-16 代理项对：  
  
-   **fn: string 的长度**。 但是，如果一个无效的或部分代理项对传递作为参数的行为**字符串长度**是不确定的。  
  
-   **fn: substring**。  
  
-   **fn： 包含**。 但是，如果部分代理项对作为值传递**包含**可能返回意外的结果，因为它可能会发现格式正确的代理项对中包含的部分代理项对。  
  
-   **fn: concat**。 但是，如果部分代理项对作为值传递**concat**会产生不正确的代理项对或部分代理项对。  
  
-   比较运算符和**按排序**子句。 比较运算符包括 +、 \<，>， \<=、 > =、 `eq`， `lt`， `gt`， `le`，和`ge`。  
  
#### <a name="distributed-query-calls-to-a-system-procedure"></a>对系统过程的分布式查询调用  
 在从一个 `OPENQUERY` 服务器对另一个服务器进行调用时，通过 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 对某些系统过程进行的分布式查询调用将失败。 在 [!INCLUDE[ssDE](../includes/ssde-md.md)] 无法发现某个过程的元数据时将出现此情况。 例如，`SELECT * FROM OPENQUERY(..., 'EXEC xp_loginfo')`。  
  
#### <a name="isolation-level-and-spresetconnection"></a>隔离级别和 sp_reset_connection  
 连接用隔离级别由客户端驱动程序按照如下方法处理：  
  
-   所有的本机驱动程序（SNAC、MDAC、ODBC）都根据 sp_reset_connection 设置隔离级别（基于应用设置）。  
  
-   对于 ADO.NET，你实质上会获得一个随机的隔离级别，这取决于你从池中获取的连接（以及应用程序是否使用不同的隔离级别）。 由于 ADO.NET 池可在内部以透明方式回收连接，你无法预测将从池中得到什么结果。  
  
-   对于 JDBC 驱动程序，你获得与 ADO.NET 相同的行为  
  
     打开连接以获取所需之后，应用程序必须始终显式设置隔离级别。  
  
     JDBC 连接可以共用，从而应用程序可获取一个随机隔离级别但并不知情。  
  
 若要保留向后兼容性，这种新行为仅适用于以 TDS 7.4 开头的较新的客户端。  
  
#### <a name="backward-compatibility"></a>Backward Compatibility  
 **新行为取决于兼容性级别**  
  
 仅当数据库兼容性级别为 110 或更高时，以下函数和运算符才具有上述新行为：  
  
-   **fn： 包含**。  
  
-   **fn: concat**。  
  
-   比较运算符和**按排序**子句  
  
 **新行为取决于函数的默认命名空间 URI**  
  
 以下函数都将新行为所述上方时，才默认命名空间 URI 对应于最终建议中的命名空间，即[ http://www.w3.org/2005/xpath-functions ](http://www.w3.org/2005/xpath-functions)。 数据库兼容性级别为 110 或更高时，默认情况下 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 将默认函数命名空间绑定到此命名空间。 但是，无论兼容性级别如何，使用此命名空间时，这些函数都将具有新行为。  
  
-   **fn:string-length**  
  
-   **fn:substring**  
  
##  <a name="KJKatmai"></a> 重大更改，在 SQL Server 2008/SQL Server 2008R2  
 本节包含 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中引入的重大更改。 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中未引入任何更改。  
  
### <a name="collations"></a>排序规则  
  
|功能|Description|  
|-------------|-----------------|  
|新排序规则|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 引入了新的排序规则，这些规则完全符合 Windows Server 2008 提供的排序规则。 这 80 个新排序规则以 *_100 版本引用表示，它们的语言准确性得到了改善。 如果为服务器或数据库选择新排序规则，请注意，具有旧客户端驱动程序的客户端可能无法识别新排序规则。 未被识别的排序规则可能会导致应用程序返回错误并失败。 请考虑以下解决方案：<br /><br /> 升级客户端操作系统，以更新基础系统排序规则。<br /><br /> 如果客户端上安装了数据库客户端软件，则可以考虑对数据库客户端软件应用服务更新。<br /><br /> 选择一个现有排序规则，该排序规则会映射到客户端上的一个代码页。|  
  
### <a name="common-language-runtime-clr"></a>公共语言运行时 (CLR)  
  
|功能|Description|  
|-------------|-----------------|  
|CLR 程序集|当数据库升级到 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 后，将自动安装 `Microsoft.SqlServer.Types` 程序集以支持新数据类型。 升级顾问规则将检测存在名称冲突的任何用户类型或程序集。 升级顾问将建议您重命名所有冲突的程序集，并重命名所有冲突的类型或在代码中使用由两部分组成的名称来引用该预先存在的用户类型。<br /><br /> 如果数据库升级检测到某个用户程序集具有冲突名称，它将自动重命名该程序集，并将数据库置于可疑模式下。<br /><br /> 如果在升级过程中存在具有冲突名称的用户类型，则不会采取特殊步骤。 升级后，旧的用户类型和新的系统类型将同时存在。 用户类型将只能通过由两部分组成的名称使用。|  
|CLR 程序集|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 会安装 .NET Framework 3.5 SP1，以更新全局程序集缓存 (GAC) 中的库。 如果在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中注册了不支持的库，则在升级到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 后，[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 应用程序可能会停止工作。 这是因为，在 GAC 中为库提供服务或升级库时并不会更新 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的程序集。 如果某一程序集存在于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库和 GAC 中，该程序集的两个副本必须完全匹配。 如果不一致，当 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] CLR 集成功能使用该程序集时，将发生错误。 有关详细信息，请参阅[支持的.NET Framework 库](../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。<br /><br /> 升级数据库之后，请使用 ALTER ASSEMBLY 语句对该程序集在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的副本提供服务或进行升级。 有关详细信息，请参阅[知识库文章 949080](https://go.microsoft.com/fwlink/?LinkId=154563)。<br /><br /> 若要检测是否在应用程序中使用了任何不支持的 .NET Framework 库，请在数据库中运行以下查询。<br /><br /> `SELECT name FROM sys.assemblies WHERE clr_name LIKE '%publickeytoken=b03f5f7f11d50a3a,%';`|  
|CLR 例程|在 CLR 用户定义函数、用户定义聚合或用户定义类型 (UDT) 内使用模拟可导致应用程序在升级到 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 后因出现错误 6522 而失败。 下列情况在 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 中成功，而在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中则失败。 针对每种情况提供了相应的解决方案。<br /><br /> CLR 用户定义函数、 用户定义聚合或使用模拟的 UDT 方法具有类型参数`nvarchar(max)`， `varchar(max)`， `varbinary(max)`， `ntext`， `text`， `image`，或大型 UDT，并且没有**DataAccessKind.Read**方法上的属性。 若要解决此问题，请添加**DataAccessKind.Read**方法属性，重新编译程序集，并重新部署例程和程序集。<br /><br /> 具有的 CLR 表值函数**Init**执行模拟的方法。 若要解决此问题将添加**DataAccessKind.Read**方法属性，重新编译程序集，并重新部署例程和程序集。<br /><br /> 具有的 CLR 表值函数**FillRow**执行模拟的方法。 若要解决此问题，请删除从模拟**FillRow**方法。 通过使用不访问外部资源**FillRow**方法。 相反，访问从外部资源**Init**方法。|  
  
### <a name="dynamic-management-views"></a>动态管理视图  
  
|“查看”|Description|  
|----------|-----------------|  
|sys.dm_os_sys_info|删除了 cpu_ticks_in_ms 和 sqlserver_start_time_cpu_ticks 列。|  
|sys.dm_exec_query_resource_semaphoressys.dm_exec_query_memory_grants|resource_semaphore_id 列不是 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中的唯一 ID。 此更改会对故障排除查询执行造成影响。 有关详细信息，请参阅[sys.dm_exec_query_resource_semaphores &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql)。|  
  
### <a name="errors-and-events"></a>错误和事件  
  
|功能|Description|  
|-------------|-----------------|  
|登录错误|在 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 中，当使用 SQL 登录名连接到配置为仅使用 Windows 身份验证的服务器时，会返回错误 18452。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，则会返回错误 18456。|  
  
### <a name="showplan"></a>Showplan  
  
|功能|Description|  
|-------------|-----------------|  
|显示计划 XML 架构|一个新**SeekPredicateNew**元素添加到显示计划 XML 架构，并将封闭 xsd 序列 (**SqlPredicatesType**) 转换为 **\<xsd:choice >** 项。 而不是一个或多个**SeekPredicate**元素，一个或多个**SeekPredicateNew**元素现在可能会显示在显示计划 XML 中。 这两种元素是相互排斥的。 **SeekPredicate**中进行维护的显示计划 XML 架构向后兼容性; 但是，查询计划中创建[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]可能包含**SeekPredicateNew**元素。 应用程序仅检索**SeekPredicate**从节点 ShowPlanXML/BatchSequence/Batch/语句/StmtSimple/QueryPlan/RelOp/IndexScan/SeekPredicates 子可能会失败，如果**SeekPredicate**元素不存在。 重写应用程序，使任一**SeekPredicate**或**SeekPredicateNew**此节点中的元素。 有关更多信息，请参见 。|  
|显示计划 XML 架构|一个新**IndexKind**属性添加到**ObjectType**中显示计划 XML 架构复杂类型。 根据 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 架构严格验证 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 计划的应用程序将失败。|  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|功能|Description|  
|-------------|-----------------|  
|ALTER_AUTHORIZATION_DATABASE DDL 事件|在[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]DDL 事件 alter_authorization_database 后触发，object 中返回的值时， **ObjectType**的实体类型的数据定义中的安全对象时此事件的 EVENTDATA xml 元素语言 (DDL) 操作是一个对象。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，则返回实际类型（例如，“table”或“function”）。|  
|CONVERT|如果传递到 CONVERT 函数的样式无效，则会在二进制转换为字符或字符转换为二进制时，返回一个错误。 在早期版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，该无效样式会设置为二进制与字符间相互转换时的默认样式。|  
|对程序集 GRANT/DENY/REVOKE EXECUTE|不能对程序集授予、拒绝或撤消“EXECUTE”权限。 此权限不起任何作用，并且现在会导致一个错误。 可以对引用程序集方法的存储过程或函数授予、拒绝或撤消“EXECUTE”权限。|  
|对系统类型 GRANT/DENY/REVOKE 权限|不能对系统类型授予、拒绝或撤消权限。 在早期版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，这些语句会成功，但是不起任何作用。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，则会返回错误。|  
|GROUP BY|GROUP BY 子句在用于分组依据列表的表达式中不能包含子查询。 在早期版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，允许这样做。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，则会返回错误 144。<br /><br /> 例如，以下代码在 SQL Server 2005 中运行成功而在 SQL Server 2008 中运行失败：<br /><br /> `DECLARE @Test TABLE(a int NOT NULL);` <br /> `INSERT INTO @Test SELECT 1 union ALL SELECT 2;` <br /> `SELECT COUNT(*)` <br /> `FROM @Test` <br /> `GROUP BY CASE WHEN a IN (SELECT t.a FROM @Test AS t)` <br /> `THEN 1 ELSE 0` <br /> `END;`|  
|OUTPUT 子句|为了防止出现不确定的行为，当某个列是通过下列方法之一定义时，OUTPUT 子句不能通过视图或内联表值函数引用该列：<br /><br /> 子查询。<br /><br /> 执行用户数据访问或系统数据访问（或者被认为执行此类访问）的用户定义函数。<br /><br /> 在定义中包含执行用户数据访问或系统数据访问的用户定义函数的计算列。<br /><br /> <br /><br /> 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 OUTPUT 子句中检测到了此类列，将引发错误 4186。 有关详细信息，请参阅[MSSQLSERVER_4186](../relational-databases/errors-events/mssqlserver-4186-database-engine-error.md)。|  
|OUTPUT INTO 子句|OUTPUT INTO 子句的目标表不能有任何已启用的触发器。|  
|precompute rank 服务器级选项|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 不支持此选项。 请尽快修改当前使用此功能的应用程序。|  
|READPAST 表提示|您不能在快照隔离下指定 READPAST 提示。<br /><br /> 在将 READ_COMMITED_SNAPSHOT 或 ALLOW_SNAPSHOT_ISOLATION 数据库选项设置为 ON 时，将忽略 READPAST 提示。 但是，如果您将 READPAST 提示与 READCOMMITTEDLOCK 相结合，则 READPAST 行为与阻止 READCOMMITTED 提示等效。|  
|sp_helpuser|在 sp_helpuser 存储过程的结果集中返回的以下列名进行了更改：<br /><br /> 组名现在是：<br />                            RoleName<br /><br /> 现在，Group_name 是：<br />                            Role_name<br /><br /> Group_id 现在是：<br />                            Role_id<br /><br /> Users_in_group 现在是：<br />                            Users_in_role|  
|透明数据加密|在 I/O 级别执行透明数据加密 (TDE)：页结构在内存中不加密，而仅在将页写入到磁盘后才对页结构进行加密。 数据库文件和日志文件均加密。 当数据库使用 TDE 时，那些跳过常规 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 机制来访问页面（例如，通过直接扫描数据或日志文件）的第三方应用程序将失败，因为文件中的数据已被加密。 此类应用程序可以利用 Windows 加密 API 来开发用来在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 外部对数据进行解密的解决方案。|  
  
### <a name="xquery"></a>XQuery  
  
|功能|Description|  
|-------------|-----------------|  
|Datetime 支持|在中[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]，数据类型`xs:time`， `xs:date`，和`xs:dateTime`没有时区支持。 时区数据会映射到 UTC 时区。 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 提供了符合标准的行为，从而导致了以下变化：<br /><br /> 将验证没有时区的值。<br /><br /> 将保留提供的时区或缺少的时区。<br /><br /> 修改了内部存储表示形式。<br /><br /> 增加了存储值的分辨率。<br /><br /> 不允许使用负年份。<br /><br /> <br /><br /> 注意：可以修改应用程序和 XQuery 表达式来利用新类型值。|  
|XQuery 和 Xpath 表达式|在[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]，以冒号开头的 XQuery 或 XPath 表达式中的步骤 (:) 允许使用。 例如，下面的语句在路径表达式中包含以冒号开头的名称测试 (`CTR02)`。<br /><br /> `SELECT FileContext.query('for n$ in //CTR return <C>{data )(n$/:CTR02)} </C>) AS Files FROM dbo.MyTable;`<br /><br /> 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，这种用法是不允许的，因为它不符合 XML 标准。 返回错误 9341。 请删除前导冒号或为名称测试指定一个前缀，例如 (n$/CTR02) 或 (n$/p1:CTR02)。|  
  
### <a name="connecting"></a>Connecting  
  
|功能|Description|  
|-------------|-----------------|  
|使用 SSL 从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 进行连接|当使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 进行连接时，将 "SERVER=shortname; FORCE ENCRYPTION=true" 用于其主题指定完全限定域名 (FQDN) 的证书的应用程序在过去由于放宽的验证而已进行了连接。 SQL Server 2008 R2 通过为证书实现 FQDN 主题增强安全性。 依赖于已放宽验证的应用程序必须采取以下措施之一：<br /><br /> 在连接字符串中使用 FQDN。<br /><br /> -此选项不需要重新编译应用程序，如果应用程序外部配置的连接字符串的 SERVER 关键字。<br /><br /> -此选项不适用于具有其连接字符串进行硬编码的应用程序。<br /><br /> -此选项不适用于自镜像的服务器将回复一个简单名称后使用数据库镜像的应用程序。|  
||为映射到 FQDN 的短名称添加别名。<br /><br /> -此选项甚至适用于具有其连接字符串进行硬编码的应用程序。<br /><br /> -此选项不适用于使用数据库镜像，因为提供程序不通过查找别名收到的故障转移伙伴名称的应用程序。|  
||为短名称签发一个证书。<br /><br /> -此选项适用于所有应用程序。|  

## <a name="Yukon"></a> SQL Server 2005 中的重大更改  

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>请参阅  
 [SQL Server 2014 中弃用的数据库引擎功能](deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014 中数据库引擎功能的行为更改](../../2014/database-engine/behavior-changes-to-database-engine-features-in-sql-server-2014.md)   
 [SQL Server 2014 中废止的数据库引擎功能](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server 数据库引擎的向后兼容性](sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
 [SQL Server 2014 中管理工具功能的中断性变更](breaking-changes-to-management-tools-features-in-sql-server-2014.md?view=sql-server-2014)  
  
