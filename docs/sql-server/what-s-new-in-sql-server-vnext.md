---
title: "SQL Server vNext 中的新增功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: "craigg-msft"
ms.author: "craigg"
manager: "jhubbard"
caps.handback.revision: 65
---
# SQL Server vNext 中的新增功能
通过将 SQL Server 的强大功能引入 Linux、基于 Linux 的 Docker 容器和 Windows，使 SQL Server 成为一个能够选择开发语言、数据类型、在本地和在云中以及跨操作系统的平台，对此，SQL Server vNext 跨出了重要的一步。

本主题概括了最新社区技术预览版 (CTP) 发行版中的新增功能，并提供了相关链接供详细了解特定功能领域的新增内容信息。

![info_tip](../sql-server/media/info-tip.png) 在 Linux 上运行 SQL Server！ 有关详细信息，请参阅：
-  [What's new for SQL Server vNext on Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-whats-new)（Linux 上 SQL Server vNext 的新增功能）
-  [SQL Server on Linux Documentation](https://docs.microsoft.com/en-us/sql/linux/)（Linux 文档上的 SQL Server）


**进行试用：**    
   -   [![从评估中心下载](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[下载 SQL Server vNext 社区技术预览版](http://go.microsoft.com/fwlink/?LinkID=829477)**


## <a name="whats-new-in-sql-server-vnext-ctp-13-february-2017"></a>SQL Server vNext CTP 1.3 中的新增功能（2017 年 2 月）
### <a name="sql-server-database-engine"></a>SQL Server 数据库引擎
- 间接检查点性能改进。
- 新增了对“无群集可用性组”的支持。
- 添加了“最小复制提交可用性组”设置。
- 可用性组现可跨 Windows-Linux 工作，从而实现跨操作系统的迁移和测试。
- 新增了对“临时表保留策略”的支持，
- New DMV SYS.DM_DB_STATS_HISTOGRAM
- 新增了对联机非聚集列存储索引生成和重新生成的支持
- 5 个新的动态管理视图，可返回有关 Linux 进程的信息。 有关详细信息，请参阅 [Linux 进程动态管理视图](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)。   
- 添加了 [sys.dm_db_stats_histogram (TRANSACT-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)，用于检查统计信息。

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- 编码提示 - 一种用于优化大型内存中表格模型处理（数据刷新）的高级功能。 若要了解详细信息，请参阅 [Analysis Services vNext 中的新增功能](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md)。 

## <a name="whats-new-in-sql-server-vnext-ctp-12-january-2017"></a>SQL Server vNext CTP 1.2 中的新增功能（2017 年 1 月）
### <a name="sql-server-database-engine"></a>SQL Server 数据库引擎
- 非聚集列存储索引现支持联机索引生成和重新生成。
- 此 CTP 还包含对数据库引擎的 bug 修复。
- 有关先前 CTP 版本中 vNext CTP 增强功能的详细列表，请参阅 [SQL Server vNext（数据库引擎）中的新增功能](../database-engine/configure-windows/what-s-new-in-sql-server-vnext-database-engine.md)。

### <a name="sql-server-r-services"></a>SQL Server R Services
- 此 CTP 中没有新的 R Services 功能。
- 有关 R Services 新增功能的详细信息（包括以前的 CTP 中的详细信息），请参阅 [SQL Server R Services 中的新增功能](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)。  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- 此 CTP 中没有新的 SSRS 功能。
- 有关 SSRS 新增功能的详细信息（包括先前版本中的详细信息），请参阅 [Reporting Services 中的新功能](../reporting-services/sql-server-reporting-services-ssrs-中的新增功能.md)。 

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- 此 CTP 中没有新的 SSAS 功能。  
- 有关详细信息，请参阅 [Analysis Services vNext 中的新增功能](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md)。  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- 此 CTP 中没有新的 SSIS 功能。
- 有关 SSIS 新增功能的详细信息（包括以前的 CTP 中的详细信息），请参阅 [Integration Services vNext 中的新增功能](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md)。  

### <a name="master-data-services-mds"></a>Master Data Services (MDS)
- 此 CTP 中没有新的 Master Data Services 功能。

##  <a name="infotipimageshiproominfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 与 SQL Server 工程团队合作 
- [堆栈溢出 (tag sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 论坛](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 报告 bug 和请求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有关 R 的一般讨论](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>另请参阅    
 + [![发行说明](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png)](SQL%20Server%20vNext%20Release%20Notes.md)[SQL Server VNext 发行说明](../sql-server/sql-server-vnext-release-notes.md)。 
+ [版本支持的功能](https://msdn.microsoft.com/library/cc645993.aspx)
 + [[硬件和软件安装要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)](Hardware%20and%20Software%20Requirements%20for%20Installing%20SQL%20Server%202016.md)
 + [安装向导](../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)
 
 + [安装程序和安装服务](Setup%20and%20Servicing%20Installation.md)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)