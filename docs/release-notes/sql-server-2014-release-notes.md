---
title: "SQL Server 2014 发行说明 | Microsoft Docs"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-server-2014
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: 100
author: byham
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0ca391c25a462a5f30d6a9bc51b4541f77adfd48
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
本发行说明文档介绍了在安装 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]或者解决其相关问题之前应该了解的一些已知问题。  
  
## <a name="top"></a>目录  
[1.0 安装之前](#BeforeInstall)  
  
[2.0 产品文档](#ProdDoc)  
  
[3.0 数据库引擎](#DBEngine)  
  
[4.0 Reporting Services](#SSRS)  
  
[5.0 Windows Azure 虚拟机上的 SQL Server 2014](#AzureVM)  
  
[6.0 Analysis Services](#SSAS)  
  
[7.0 Data Quality Services](#DQS)  
  
[8.0 升级顾问](#UA)  
  
## <a name="BeforeInstall"></a>1.0 安装之前  
  
### <a name="11-limitations-and-restrictions-in-sql-server-2014-rtm"></a>1.1 SQL Server 2014 RTM 中的限制和局限  
  
#### <a name="111-general-limitations-and-restrictions"></a>1.1.1 一般限制和局限  
  
1.  不支持从 SQL Server 2014 CTP 1 升级到 SQL Server 2014 RTM。  
  
2.  不支持将 SQL Server 2014 CTP 1 与 SQL Server 2014 RTM 并行安装。  
  
3.  不支持将 SQL Server 2014 CTP 1 数据库附加到 SQL Server 2014 RTM 或将 SQL Server 2014 CTP 1 数据库还原到 SQL Server 2014 RTM。  
  
**解决方法：** 无。  
  
#### <a name="12-considerations-for-upgrading-sql-server-2014-ctp-2-to-sql-server-2014-rtm-and-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2 将 SQL Server 2014 CTP 2 升级到 SQL Server 2014 RTM 和从 SQL Server 2014 RTM 降级到 SQL Server 2014 CTP 2 的注意事项  
  
#### <a name="121-upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm-is-fully-supported"></a>1.2.1 完全支持从 SQL Server 2014 CTP 2 升级到 SQL Server RTM  
具体而言，您可以：  
  
1.  将 SQL Server 2014 CTP 2 数据库附加到 SQL Server 2014 RTM 实例。  
  
2.  将在 SQL Server 2014 CTP 2 上执行的数据库备份还原到 SQL Server 2014 RTM 实例。  
  
3.  就地升级到 SQL Server 2014 RTM。  
  
4.  滚动升级到 SQL Server 2014 RTM。 在启动滚动升级前，您需要切换到手动故障转移模式。 有关详细信息，请参考 [在停机时间和数据丢失最少的情况下升级和更新可用性组服务器](http://msdn.microsoft.com/library/dn178483.aspx) 。  
  
5.  通过 SQL Server 2014 CTP 2 中安装的事务性能收集组收集的数据不能通过 SQL Server 2014 RTM 中的 SQL Server Management Studio 查看，反之亦然。 使用 SQL Server 2014 CTP 2 中的 SQL Server Management Studio 可查看通过 SQL Server 2014 CTP 2 中安装的收集组收集的数据，使用 SQL Server 2014 RTM 中的 SQL Server Management Studio 可查看通过 SQL Server 2014 RTM 中安装的收集组收集的数据。  
  
### <a name="122-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2.2 从 SQL Server 2014 RTM 降级到 SQL Server 2014 CTP 2  
不支持此设置。  
  
**解决方法：** 没有针对降级的解决方法。 我们建议您在升级到 SQL Server 2014 RTM 之前备份数据库。  
  
![与“返回首页”链接一起使用的箭头图标](../release-notes/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[顶部](#top)  
  
## <a name="13-incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>1.3 SQL Server 2014 介质/ISO/CAB 上 StreamInsight 客户端的版本不正确  
错误版本的 StreamInsight.msi 和 StreamInsightClient.msi 位于 SQL Server 介质/ISO/CAB 上的以下路径中 (StreamInsight\\\<Architecture\>\\\<Language ID\>)。  
  
**解决方法：** 从 [SQL Server 2014 功能包下载页](http://go.microsoft.com/fwlink/?LinkID=306709)下载并安装正确的版本。  
  
## <a name="ProdDoc"></a>2.0 产品文档  
  
### <a name="21-report-builder-content-is-not-available-in-some-languages"></a>2.1 不提供某些语言的报表生成器内容  
**问题：** 不提供以下语言的报表生成器内容。  
  
-   希腊语 (el-GR)  
  
-   挪威语（博克马尔）(nb-NO)  
  
-   芬兰语 (fi-FI)  
  
-   丹麦语 (da-DK)  
  
在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中，此内容在产品随附的 CHM 文件中提供并且提供这些语言的内容。 这些 CHM 文件不再随产品一起提供，并且报表生成器内容仅在 MSDN 上提供。 MSDN 不支持这些语言。 报表生成器也已从 TechNet 中删除并且在这些支持的语言中不再提供。  
  
**解决方法：** 无。  
  
### <a name="22-powerpivot-content-is-not-available-in-some-languages"></a>2.2 某些语言版本不提供 PowerPivot 内容。  
**问题：** 不提供以下语言的 Power Pivot 内容。  
  
-   希腊语 (el-GR)  
  
-   挪威语（博克马尔）(nb-NO)  
  
-   芬兰语 (fi-FI)  
  
-   丹麦语 (da-DK)  
  
-   捷克语 (cs-CZ)  
  
-   匈牙利语 (hu-HU)  
  
-   荷兰语（荷兰）(nl-NL)  
  
-   波兰语 (pl-PL)  
  
-   瑞典语 (sv-SE)  
  
-   土耳其语 (tr-TR)  
  
-   葡萄牙语（葡萄牙）(pt-PT)  
  
在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中，已在 TechNet 上提供此内容并且提供这些语言的内容。 此内容已从 TechNet 中删除并且不再提供这些支持的语言的内容。  
  
**解决方法：** 无。  
  
![与“返回首页”链接一起使用的箭头图标](../release-notes/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[顶部](#top)  
  
## <a name="DBEngine"></a>3.0 数据库引擎  
  
### <a name="31-changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>3.1 SQL Server 2014 RTM 中针对 Standard Edition 所做的更改  
SQL Server 2014 Standard 具有以下更改：  
  
-   缓冲池扩展功能允许使用的最大大小为所配置内存的 4 倍。  
  
-   最大内存从 64GB 增加到 128GB。  
  
### <a name="32-in-memory-oltp-issues"></a>3.2 内存中 OLTP 问题  
  
#### <a name="321-memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>3.2.1 内存优化顾问将默认约束标记为不兼容  
**问题：** SQL Server Management Studio 中的内存优化顾问将所有默认约束标记为不兼容。 内存优化表中不是所有默认约束都支持；顾问并不区分支持和不支持的默认约束类型。 支持的默认约束包括本机编译的存储过程中的所有常量、表达式和内置函数。 要查看本机编译的存储过程中支持的函数的列表，请参阅 [本机编译的存储过程中支持的构造](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx)(#本机编译的存储过程中支持的构造)。  
  
**解决方法：** 如果要使用顾问识别阻塞程序，请忽略兼容的默认约束。 要使用内存优化顾问迁移具有兼容默认约束但没有其他阻塞程序的表，请按照以下步骤操作：  
  
1.  从表定义中删除默认约束。  
  
2.  使用顾问生成对表的迁移脚本。  
  
3.  在迁移脚本中添加回默认约束。  
  
4.  执行迁移脚本。  
  
#### <a name="322-informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>3.2.2 信息性消息“文件访问被拒绝”在 SQL Server 2014 错误日志中不正确地报告为错误  
**问题：** 在重新启动的服务器具有包含内存优化表的数据库时，在 SQL Server 2014 错误日志中可能会看到以下类型的错误消息：  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
  
实际上这是一条信息性消息，不需要用户执行任何操作。  
  
**解决方法：** 无。 这是一条信息性消息。  
  
#### <a name="323-missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>3.2.3 缺少索引详细信息不正确地报告内存优化表的包含列  
**问题：** 如果 SQL Server 2014 检测到对内存优化表的查询缺少索引，它会在 SHOWPLAN_XML 中报告缺少索引，并在缺少索引 DMV 中报告缺少索引，如 sys.dm_db_missing_index_details。 在某些情况下，缺少索引详细信息将包含有包含列。 因为所有列都是使用内存优化表的所有索引隐式包含的，所以不允许使用内存优化索引显式指定包含列。  
  
**解决方法：** 不使用内存优化表索引指定 INCLUDE 字句。  
  
#### <a name="324-missing-index-details-omit-missing-indexes-if-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>3.2.4 哈希索引存在但不适用于查询时缺失索引详细信息忽略缺失索引  
**问题：** 如果查询中引用的内存优化表的列存在哈希索引，但该索引不能用于查询，SQL Server 2014 将不会始终在 SHOWPLAN_XML 和 DMV sys.dm_db_missing_index_details 中报告缺失索引。  
  
特别是查询包含涉及索引键列子集的相等谓词或包含涉及索引键列的相等谓词时，哈希索引不能原样使用，这时就需要不同的索引才能有效地执行查询。  
  
**解决方法：** 在使用哈希索引时，检查查询和查询计划，确保查询可以从对索引键子集的 Index Seek 操作或对不等谓词的 Index Seek 操作获益。 如果需要查找索引键子集，请使用非聚集索引或对需要查找的列使用哈希索引。 如果需要查找不等谓词，请使用非聚集索引而不是哈希索引。  
  
#### <a name="325-failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>3.2.5 在同一查询中使用内存优化表和内存优化表变量时，如果数据库选项 READ_COMMITTED_SNAPSHOT 设置为 ON，就会失败  
**问题：** 如果数据库选项 READ_COMMITTED_SNAPSHOT 设置为 ON，当在用户事务外的同一语句中访问内存优化表和内存优化表变量时，可能会看到这一错误消息：  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**解决方法：** 用表变量使用表提示 WITH (SNAPSHOT) 或者将数据库选项 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT 设置为 ON，使用以下语句：  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="326-procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>3.2.6 本机编译存储过程的过程和查询执行统计信息按 1000 倍记录工作线程时间  
**问题：** 使用 sp_xtp_control_proc_exec_stats 或 sp_xtp_control_query_exec_stats 启用本机编译存储过程的过程或查询执行统计信息收集后，会看到 *_worker_time 在 DMV sys.dm_exec_procedure_stats 和 sys.dm_exec_query_stats 中按 1000 倍报告。 工作线程时间少于 500 毫秒的查询执行将按 worker_time 为 0 报告。  
  
**解决方法：** 无。 对于本机编译存储过程中短时间运行的查询，不要依赖执行状态 DMV 中报告的 worker_time。  
  
#### <a name="327-error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>3.2.7 包含长表达式的本机编译存储过程使用 SHOWPLAN_XML 的错误  
**问题：** 如果本机编译存储过程包含长表达式，使用 T-SQL 选项 SET SHOWPLAN_XML ON 或使用 Management Studio 中的“显示估计的执行计划”选项获取过程的 SHOWPLAN_XML 可能导致以下错误：  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**解决方法：** 有两个建议的解决方法：  
  
1.  为表达式添加括号，类似以下示例：  
  
    不是：  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    编写：  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  使用稍微简化的表达式为显示计划目的创建第二个过程，该计划的形状应大致相同。 例如，不是：  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    编写：  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="328-using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>3.2.8 在本机编译存储过程中对 DATEPART 和相关函数使用字符串参数或变量会导致错误  
**问题：** 在对本机编译存储过程中的内置函数 DATEPART、DAY、MONTH 和 YEAR 使用具有字符串数据类型（如 (var)char 或 n(var)char）的参数或变量时，会显示一条错误消息，说明本机编译存储过程不支持数据类型 datatype。  
  
**解决方法：** 将字符串参数或变量分配给一个新的 datetime2 类型的变量，在函数 DATEPART、DAY、MONTH 或 YEAR 中使用该变量。 例如：  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="329-native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>3.2.9 本机编译顾问错误标记 DELETE FROM 子句  
**问题：** 本机编译顾问将存储过程内的 DELETE FROM 子句错误标记为不兼容。  
  
**解决方法：** 无。  
  
### <a name="33-register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>3.3 通过 SSMS 注册会为 DAC 元数据添加不匹配的 ID  
**问题：** 通过 SQL Server Management Studio 注册或删除数据层应用程序包 (.dacpac) 时，sysdac* 表不会正确更新以允许用户查询数据库的 dacpac 历史记录。  sysdac_history_internal 和 sysdac_instances_internal 的 instance_id 不匹配，无法联接。  
  
**解决方法：** 此问题已通过 [数据层应用程序框架](https://www.microsoft.com/download/details.aspx?id=42295)(#数据层应用程序框架) 的功能包再分发得到修复。  应用更新后，所有的新历史记录条目都将使用 sysdac_instances_internal 表中为 instance_id 列出的值。  
  
如果已经出现 instance_id 值不匹配的问题，纠正不匹配值的唯一方法是以拥有 MSDB 数据库写入权限的用户身份连接到服务器并更新 instance_id 值使其匹配。  如果同一数据库有多个注册和撤消注册事件，可能需要查看时间/日期来确定与当前 instance_id 值匹配的记录。  
  
1.  在 SQL Server Management Studio 中使用对 MSDB 具有更新权限的登录名连接到服务器。  
  
2.  使用 MSDB 数据库打开一个新查询。  
  
3.  运行此查询查看所有活动的 DAC 实例。  找到你要更正的实例并记下 instance_id：  
  
    `select * from` sysdac_instances_internal  
  
4.  运行此查询可查看所有历史记录条目：  
  
    `select * from` sysdac_history_internal  
  
5.  确定与待修复实例对应的行  
  
6.  将 sysdac_history_internal.instance_id 值更新为在步骤 3 中记下的值（来自 sysdac_instances_internal 表）：  
  
    `update` sysdac_history_internal `set` instance_id = '\<来自步骤 3 的值\>' `where` \<与要更新的行匹配的表达式\>  
  
![与“返回首页”链接一起使用的箭头图标](../release-notes/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[顶部](#top)  
  
## <a name="SSRS"></a>4.0 Reporting Services  
  
### <a name="41-the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>4.1 SQL Server 2012 Reporting Services 本机模式报表服务器不能与 SQL Server 2014 Reporting Services SharePoint 组件并行运行  
**问题：**同一服务器上安装了 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 组件时 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本机模式 Windows 服务“SQL Server Reporting Services”(ReportingServicesService.exe) 无法启动。  
  
**解决方法：** 卸载 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 组件并重新启动 Microsoft SQL Server 2012 Reporting Services Windows 服务。  
  
**详细信息：**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]本机模式不能与以下组件之一并行运行：  
  
-   用于 SharePoint 产品的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共享服务  
  
并行安装会阻止 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本机模式 Windows 服务启动。 在 Windows 事件日志中将看到类似以下的错误消息：  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
有关详细信息，请参阅 [SQL Server 2014 Reporting Services 提示、技巧和故障排除](http://go.microsoft.com/fwlink/?LinkID=391254)。  
  
### <a name="42-required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>4.2 多节点 SharePoint 场到 SQL Server 2014 Reporting Services 所需的升级顺序  
**问题：** 如果 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共享服务实例在 SharePoint 产品的所有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序实例前升级，多节点场中的报表呈现将失败。  
  
**解决方法：** 在多节点 SharePoint 场中：  
  
1.  首先升级 SharePoint 产品的所有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序实例。  
  
2.  然后再升级 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共享服务的所有实例。  
  
有关详细信息，请参阅 [SQL Server 2014 Reporting Services 提示、技巧和故障排除](http://go.microsoft.com/fwlink/?LinkID=391254)。  
  
![与“返回首页”链接一起使用的箭头图标](../release-notes/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[顶部](#top)  
  
## <a name="AzureVM"></a>5.0 Windows Azure 虚拟机上的 SQL Server 2014 RTM  
  
### <a name="51-the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>5.1 在 Windows Azure 中配置可用性组侦听器时添加 Azure 副本向导返回错误  
**问题：** 如果可用性组具有侦听器，在您尝试在 Windows Azure 中配置可用性组侦听器时添加 Azure 副本向导将返回错误。  
  
这是因为可用性组侦听器需要在每个子网托管可用性组中分配一个 IP 地址，包括 Azure 子网。  
  
**解决方法：**  
  
1.  在“侦听器”页上，在将托管可用性组副本的 Azure 子网中为可用性组侦听器分配一个空闲的静态 IP 地址。  
  
    这样，向导将在 Windows Azure 中完成添加副本的工作。  
  
2.  向导完成后，您将需要按照 [Windows Azure 中 AlwaysOn 可用性组的侦听器配置](http://msdn.microsoft.com/library/dn376546.aspx)中所述在 Windows Azure 中完成侦听器配置。  
  
![与“返回首页”链接一起使用的箭头图标](../release-notes/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[顶部](#top)  
  
## <a name="SSAS"></a>6.0 Analysis Services  
  
### <a name="61-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>6.1 必须为使用 SQL Server 2014 配置的 SharePoint 2010 新场下载、安装和注册 MSOLAP.5  
**问题：**  
  
-   对于使用 SQL Server 2014 RTM 部署配置的 SharePoint 2010 场，PowerPivot 工作簿无法连接到数据模型，因为未安装连接字符串中引用的访问接口。  
  
**解决方法：**  
  
1.  从 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能包下载 MSOLAP.5 访问接口。 将访问接口安装在运行 Excel Services 的应用程序服务器上。 有关详细信息，请参阅“用于 Microsoft SQL Server 2012 SP1 的 Microsoft Analysis Services OLE DB 访问接口” [Microsoft SQL Server 2012 SP1 功能包](http://www.microsoft.com/download/details.aspx?id=35580)部分。  
  
2.  将 MSOLAP.5 注册为 SharePoint Excel Services 中的受信任数据访问接口。 有关详细信息，请参阅 [“将 MSOLAP.5 添加为 Excel Services 中的受信任数据访问接口”](http://technet.microsoft.com/library/hh758436.aspx)。  
  
**详细信息：**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包括 MSOLAP.6。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿使用 MSOLAP.5。 如果运行 Excel Services 的计算机上没有安装 MSOLAP.5，Excel Services 就无法加载数据模型。  
  
### <a name="62-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>6.2 必须为使用 SQL Server 2014 配置的 SharePoint 2013 新场下载、安装和注册 MSOLAP.5  
**问题：**  
  
-   对于使用 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 部署配置的 SharePoint 2013 场，引用 MSOLAP.5 访问接口的 Excel 工作簿无法连接到表格数据模型，因为未安装连接字符串中引用的访问接口。  
  
**解决方法：**  
  
1.  从 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能包下载 MSOLAP.5 访问接口。 将访问接口安装在运行 Excel Services 的应用程序服务器上。 有关详细信息，请参阅“用于 Microsoft SQL Server 2012 SP1 的 Microsoft Analysis Services OLE DB 访问接口” [Microsoft SQL Server 2012 SP1 功能包](http://www.microsoft.com/download/details.aspx?id=35580)部分。  
  
2.  将 MSOLAP.5 注册为 SharePoint Excel Services 中的受信任数据访问接口。 有关详细信息，请参阅 [“将 MSOLAP.5 添加为 Excel Services 中的受信任数据访问接口”](http://technet.microsoft.com/library/hh758436.aspx)。  
  
**详细信息：**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包括 MSOLAP.6。 但 SQL Server 2014 PowerPivot 工作簿使用 MSOLAP.5。 如果运行 Excel Services 的计算机上没有安装 MSOLAP.5，Excel Services 就无法加载数据模型。  
  
### <a name="63-corrupt-data-refresh-schedules"></a>6.3 损坏数据刷新计划  
**问题：**  
  
-   更新刷新计划后计划损坏且不可用。  
  
**解决方法：**  
  
1.  在 Microsoft Excel 中，清除自定义高级属性。 请参阅以下知识库文章的“解决方法”部分： [KB 2927748](http://support.microsoft.com/kb/2927748)。  
  
**详细信息：**  
  
-   为工作簿更新数据刷新计划时，如果刷新计划的序列化长度小于原有计划，则缓冲区大小不会正确更新，并且新计划信息将与旧计划信息合并，导致计划损坏。  
  
![与“返回首页”链接一起使用的箭头图标](../release-notes/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[顶部](#top)  
  
## <a name="DQS"></a>7.0 Data Quality Services  
  
### <a name="71-no-cross-version-support-for-data-quality-services-in-master-data-services"></a>7.1 Master Data Services 中没有对 Data Quality Services 的跨版本支持  
**问题：** 不支持以下方案：  
  
-   Master Data Services 2014 承载在安装了 Data Quality Services 2012 的 SQL Server 2012 中的 SQL Server 数据库引擎数据库中。  
  
-   Master Data Services 2012 承载在安装了 Data Quality Services 2014 的 SQL Server 2014 中的 SQL Server 数据库引擎数据库中。  
  
**解决方法：** 使用相同版本的 Master Data Services 作为数据库引擎数据库和 Data Quality Services。  
  
![与“返回首页”链接一起使用的箭头图标](../release-notes/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[顶部](#top)  
  
## <a name="UA"></a>8.0 升级顾问问题  
  
### <a name="81--sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>8.1 SQL Server 2014 升级顾问报告与 SQL Server Reporting Services 不相关的升级问题  
**问题：**SQL Server 2014 介质附带的 SQL Server 升级顾问 (SSUA) 在分析 SQL Server Reporting Services 服务器时不正确地报告多个错误。  
  
**解决方法：**[SQL Server 2014 SSUA](http://go.microsoft.com/fwlink/?LinkID=306709)(#sql-server-2014-ssua) 功能包中提供的 SQL Server 升级顾问中修复了此问题。  
  
### <a name="82--sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>8.2 SQL Server 2014 升级顾问在分析 SQL Server Integration Services 服务器时报告错误  
**问题：** SQL Server 2014 介质附带的 SQL Server 升级顾问 (SSUA) 在分析 SQL Server Integration Services 服务器时报告错误。  向用户显示的错误如下：  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**解决方法：**[SQL Server 2014 SSUA](http://go.microsoft.com/fwlink/?LinkID=306709)(#sql-server-2014-ssua) 功能包中提供的 SQL Server 升级顾问中修复了此问题。  
  
![与“返回首页”链接一起使用的箭头图标](../release-notes/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[顶部](#top)  
  

