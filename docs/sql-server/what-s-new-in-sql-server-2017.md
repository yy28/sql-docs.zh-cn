---
title: "什么 &#39; s SQL Server 自 2017 年中的新增功能 |Microsoft 文档"
ms.custom: 
ms.date: 05/23/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 1d363db8e8bd0e1460cdea3c3a7add68e48714c9
ms.openlocfilehash: 25d81efe1b915f0e4ddc5eab2feb4142ad2ceb8f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/05/2017

---
# <a name="what39s-new-in-sql-server-2017"></a>什么 &#39; s SQL Server 自 2017 年中的新增功能
SQL Server 2017 跨出了重要的一步，它力求通过将 SQL Server 的强大功能引入 Linux、基于 Linux 的 Docker 容器和 Windows，使 SQL Server 成为一个提供开发语言、数据类型、本地开发和云端开发，以及跨操作系统开发选项的平台。

本主题概括了最新社区技术预览版 (CTP) 发行版中的新增功能，并提供了相关链接供详细了解特定功能领域的新增内容信息。

![info_tip](../sql-server/media/info-tip.png) 在 Linux 上运行 SQL Server！ 有关详细信息，请参阅：
-  [在 Linux 上的 SQL Server 2017 的新增功能](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)
-  [SQL Server on Linux Documentation](https://docs.microsoft.com/sql/linux/)


**进行试用：**    
   -   [![从评估中心下载](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[下载 SQL Server 自 2017 年 1 社区技术预览版](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="whats-new-in-sql-server-2017-ctp-21-may-2017"></a>SQL Server 2017 CTP 2.1（2017 年 5 月）中的新增功能
### <a name="sql-server-database-engine"></a>SQL Server 数据库引擎  
- 新 DMF， [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)，引入公开摘要级别的特性和事务日志文件的信息; 用于监视事务日志的运行状况。  
- 此 CTP 包含对数据库引擎的 bug 修复和性能改进。
- 有关自 2017 年 1 的详细列表 CTP 增强功能在以前的 CTP 版本，请参阅[What's New in SQL Server 2017 （数据库引擎）](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)。

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- SQL Server Reporting Services 不再可用于通过截至 CTP 2.1 的 SQL Server 安装程序安装。
- 批注现可用于报表。 通过批注，可向报表中的内容添加透视图并与组织中的其他人进行协作。 还可在批注中包含附件。
- 有关 SSRS 新增功能的详细信息（包括先前版本中的详细信息），请参阅 [Reporting Services 中的新功能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。 
- 有关 Power BI 报表服务器的信息，请参阅[开始使用 Power BI 报表服务器](https://powerbi.microsoft.com/documentation/reportserver-get-started/)。

### <a name="sql-server-machine-learning-services"></a>SQL Server 机器学习服务
- 在此 CTP 中没有新机器学习服务功能。
- 有关更详细的机器学习服务新增功能的新信息，包括从以前的 Ctp 详细信息请参阅[What's New in SQL Server 计算机学习 Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。  

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- 此 CTP 中没有新的 SSAS 功能。  
- 有关改进和 bug 修复，此版本中的更多详细信息，请参阅[What's New in SQL Server 自 2017 年 Analysis Services](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)。  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
-   你现在可以使用**Use32BitRuntime**参数。
-   日志记录的性能得到了改进。
- 有关更多详细 SSIS 新增功能的新信息，包括从以前的 Ctp 详细信息请参阅[What's New in SQL Server 自 2017 年 Integration Services](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)。  

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="whats-new-in-sql-server-2017-ctp-20-april-2017"></a>SQL Server 2017 CTP 2.0（2017 年 4 月）中的新增功能
### <a name="sql-server-database-engine"></a>SQL Server 数据库引擎
- **可恢复的联机索引重新生成**。 通过可恢复的联机索引重新生成，可从发生故障后联机索引重新生成操作停止处恢复该操作。 例如，副本的故障转移或磁盘空间不足的情况。 还可暂停操作，随后再恢复联机索引重新生成操作。 例如，可能需要暂时释放系统资源，以便执行高优先级任务或在其他维护时段完成索引重新生成操作（如果可用的维护时段太短，不足以处理大型表格）。 最后一点，可恢复的联机索引重新生成操作不需要大量的日志空间，这允许在可恢复的重新生成操作运行时执行日志截断。 请参阅[ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)和[联机索引操作准则](../relational-databases/indexes/guidelines-for-online-index-operations.md)。
- **ALTER DATABASE SCOPED CONFIGURATION IDENTITY_CACHE 选项**。 向 ALTER DATABASE SCOPED CONFIGURATION T-SQL 语句添加了新的选项 IDENTITY_CACHE。 此选项设置为“关”时，如果服务器意外重启或故障转移到辅助服务器，标识列的值中可避免出现空白。 请参阅[ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。  
- CLR 在 .NET Framework 中使用代码访问安全性 (CAS)（不可再作为安全边界）。 CLR 程序集使用创建`PERMISSION_SET = SAFE`可能能够访问外部系统资源、 调用非托管的代码，并获取 sysadmin 权限。 开头[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]、`sp_configure`选项调用`clr strict security`引入的增强 CLR 程序集的安全性。 `clr strict security`默认情况下，启用并将`SAFE`和`EXTERNAL_ACCESS`程序集就像它们被标记`UNSAFE`。 `clr strict security`选项可禁用为了向后兼容，但不是建议这样做。 Microsoft 建议所有程序集进行签名的证书或非对称密钥与相应的登录名已被授予`UNSAFE ASSEMBLY`master 数据库中的权限。 有关详细信息，请参阅[CLR 严格的安全](../database-engine/configure-windows/clr-strict-security.md)。  
- 用于多对多关系建模的图形数据库功能。 这包括新[CREATE TABLE](../t-sql/statements/create-table-sql-graph.md)创建节点和边缘表，以及关键字的语法[匹配](../t-sql/queries/match-sql-graph.md)的查询。 有关详细信息，请参阅[图形处理与 SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md)。   
- 自动优化是一种数据库功能，提供对潜在查询性能问题的深入了解，它可以提出解决方案并自动解决已标识的问题。 自动优化[!INCLUDE[ssnoversion](../includes/ssnoversion.md)]，无论何时潜在的性能问题检测到，并使你能够应用的纠正措施，通知你，或允许[!INCLUDE[ssde](../includes/ssde-md.md)]自动修复性能问题。 有关详细信息，请参阅[自动优化](../relational-databases/automatic-tuning/automatic-tuning.md)。  
-    用于改进计划质量的批处理模式自适应联接（数据库兼容级别为 140）。
-    用于改进计划质量的多语句 T-SQL TVF 交错执行（数据库兼容级别为 140）。
- 查询存储现在还可以跟踪等待统计摘要信息。 跟踪等待统计信息类别，每个查询存储中的查询使性能疑难解答的体验，并提供更多深入了解工作负荷性能和其瓶颈，同时保留关键的 Query Store 优势的下一个级别。
- 在属于可用性组的数据库（包括属于同一实例的数据库）中，针对所有跨数据库事务的 AlwaysOn 可用性组的 DTC 支持。 有关详细信息，请参阅[事务的 Alwayson 可用性组和数据库镜像](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)
- 新建一列**modified_extent_page_count**中引入[sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)来跟踪中的数据库的每个数据库文件差异更改。
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md)现在支持加载到的用户使用的默认文件组以外的文件组的表**ON**关键字。
- SQL Server 安装程序支持最多指定初始 tempdb 文件大小**256 GB (262144 MB)**每个文件以及一条警告如果文件大小设置为值大于**1 GB**和如果 IFI 未启用。
- 新的动态管理视图 (DMV) [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md)引入来跟踪每个数据库版本存储使用情况。
- 新 DMV [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)引入来公开类似于 DBCC LOGINFO VLF 信息。
- DBCC CLONEDATABASE 将在克隆时刷新运行时统计信息，避免遗漏数据库克隆中的查询存储运行时统计信息。 此外，进一步增强了 DBCC CLONEDATABASE 以支持和克隆全文索引。
- 系统版本控制临时表现在支持级联删除和级联更新。
- 此 CTP 包含对数据库引擎的 bug 修复。
- 有关自 2017 年 1 的详细列表 CTP 增强功能在以前的 CTP 版本，请参阅[What's New in SQL Server 2017 （数据库引擎）](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)。   

### <a name="sql-server-machine-learning-services"></a>SQL Server 机器学习服务
- SQL Server R Services 有了一个新名称，用于反映对 CTP 2.0 中的 Python 语言的支持。 现可使用 SQL Server 机器学习服务（数据库内）在 SQL Server 中运行 R 或 Python 脚本。 或者安装 Microsoft 机器学习服务器（独立），以部署和使用不需要 SQL Server 的 R 和 Python 模型。 
- 这两个平台都包括用于分布式机器学习的 MicrosoftML 新算法以及 Microsoft R 的最新版本（版本 9.1.0）。
- 有关详细信息，请参阅[机器学习的最近更新](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-14-march-2017"></a>SQL Server 2017 CTP 1.4（2017 年 3 月）中的新增功能
### <a name="sql-server-database-engine"></a>SQL Server 数据库引擎
- 此 CTP 中没有新的数据库引擎功能。
- 此 CTP 包含对数据库引擎的 bug 修复。
- 有关自 2017 年 1 的详细列表 CTP 增强功能在以前的 CTP 版本，请参阅[What's New in SQL Server 2017 （数据库引擎）](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)。

### <a name="sql-server-r-services"></a>SQL Server R Services
- 此 CTP 中没有新的 R Services 功能。
- 有关 R Services 新增功能的详细信息（包括以前的 CTP 中的详细信息），请参阅 [SQL Server R Services 中的新增功能](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)。  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- 此 CTP 中没有新的 SSRS 功能。
- 有关 SSRS 新增功能的详细信息（包括先前版本中的详细信息），请参阅 [Reporting Services 中的新功能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。 

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- 此 CTP 中没有新的 SSAS 功能。  
- 有关详细信息，包括新的 Analysis Services 的 SSDT 和 SSMS，最新预览版本中的新增功能，请参阅[What's New in Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)。  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- 此 CTP 中没有新的 SSIS 功能。
- 有关更多详细 SSIS 新增功能的新信息，包括从以前的 Ctp 详细信息请参阅[What's New in Integration Services 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)。  

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-13-february-2017"></a>SQL Server 2017 CTP 1.3（2017 年 2 月）中的新增功能
### <a name="sql-server-database-engine"></a>SQL Server 数据库引擎
- 间接检查点性能改进。
- 新增了对“无群集可用性组”的支持。
- 添加了“最小复制提交可用性组”设置。
- 可用性组现可跨 Windows-Linux 工作，从而实现跨操作系统的迁移和测试。
- 添加的临时表保留策略支持。 有关详细信息，请参阅[管理保留历史数据的系统版本控制的临时表中](../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md#using-temporal-history-retention-policy-approach)。
- New DMV SYS.DM_DB_STATS_HISTOGRAM
- 新增了对联机非聚集列存储索引生成和重新生成的支持
- 5 个新的动态管理视图，可返回有关 Linux 进程的信息。 有关详细信息，请参阅 [Linux 进程动态管理视图](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)。   
- 添加了[sys.dm_db_stats_histogram (TRANSACT-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) ，用于检查统计信息。

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- 编码提示 - 一种用于优化大型内存中表格模型处理（数据刷新）的高级功能。 若要了解详细信息，请参阅[What's New in Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)。 


![horizontal_bar](../sql-server/media/horizontal-bar.png)

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 与 SQL Server 工程团队合作 
- [堆栈溢出 (tag sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 论坛](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 报告 bug 和请求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有关 R 的一般讨论](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>另请参阅    
- ![发行说明](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) [SQL Server 自 2017 年 1 发行说明](../sql-server/sql-server-2017-release-notes.md)。 
- [版本支持的功能](https://msdn.microsoft.com/library/cc645993.aspx)
- [硬件和软件安装要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [SQL Server 安装向导](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [安装 SQL Server 维护服务更新](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)

