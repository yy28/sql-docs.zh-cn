---
title: "SQL Server vNext 发行说明 | Microsoft Docs"
ms.custom: 
ms.date: 03/12/2017
ms.prod: sql-vnext
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: craigg-msft
ms.author: craigg
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 93d6640c3842f36f1da10b035ae32b1f0dfc027b
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-vnext-release-notes"></a>SQL Server vNext 发行说明
本主题介绍 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的限制和问题。

- 若要了解此版本中的新增功能，请参阅 [SQL Server vNext 中的新增功能](../sql-server/what-s-new-in-sql-server-vnext.md)。
- 不断发展的新文档平台上发布了[Linux 上的 SQL Server 发行说明](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes) 。
- [SQL Server Reporting Services 发行说明](../reporting-services/reporting-services-release-notes.md) 发布于 Reporting Services 部分。

 **进行试用：**    
   -   [![从评估中心下载](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  从 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 评估中心 **[下载](http://go.microsoft.com/fwlink/?LinkID=829477)**


## <a name="sql-server-vnext-ctp-14-march--2017"></a>SQL Server vNext CTP 1.4（2017 年 3 月）
### <a name="supported-installation-scenarios-ctp-14"></a>支持的安装方案 (CTP 1.4)

### <a name="documentation-ctp-14"></a>文档 (CTP 1.4)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过**适用于**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-13-february--2017"></a>SQL Server vNext CTP 1.3（2017 年 2 月）
### <a name="supported-installation-scenarios-ctp-13"></a>支持的安装方案 (CTP 1.3)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 仅作为测试版本。  不支持生产部署。 建议在虚拟机上安装和测试 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 。

### <a name="documentation-ctp-13"></a>文档 (CTP 1.3)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过**适用于**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SQL Server Integration Services (SSIS) (CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>此 CTP 版本不支持 CDC 组件
-   **问题和对客户的影响**：此 CTP 版本不支持 CDC 控制任务、CDC 源和 CDC 拆分器。
-   **解决方法：**没有解决方法。


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-12-january--2017"></a>SQL Server vNext CTP 1.2（2017 年 1 月）
### <a name="supported-installation-scenarios-ctp-12"></a>支持的安装方案 (CTP 1.2)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 仅作为测试版本。  不支持生产部署。 建议在虚拟机上安装和测试 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 。

### <a name="sql-server-database-engine-ctp-12"></a>SQL Server 数据库引擎 (CTP 1.2)
- **问题和对客户的影响：** 在某些情况下，MSSQLSERVER 服务会一直处于“正在启动”状态。
- **解决方法：** 要解决此问题：
  -  需在 `mssqlserver` 服务和 `keyiso` 服务之间创建依赖关系。 执行此操作的一种方法是从提升的命令提示符下运行以下命令： `sc config mssqlserver depend= keyiso`
  - 重新启动计算机。

### <a name="documentation-ctp-12"></a>文档 (CTP 1.2)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过**适用于：**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SQL Server Integration Services (SSIS) (CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>如果安装了 SSIS Scale Out，删除 SSIS 目录可能会失败
**问题和对客户的影响**：如果计算机上安装了 SSIS Scale Out 功能，删除 SSISDB 目录数据库可能会失败，错误如下：“无法删除登录名‘login’  ，因为此用户当前已登录”。
   
**解决方法**：
-   在 Scale Out Master 计算机上，运行命令“services.msc”，打开“服务”窗口。 停止 SQL Server Integration Services Cluster Master 服务。
-   在连接到主服务器的 Scale Out Worker 计算机上，运行命令“services.msc”，打开“服务”窗口。 停止 SQL Server Integration Services Cluster Worker 服务。

现在可以删除 SSISDB 目录数据库。

### <a name="sql-server-master-data-services-ctp-12"></a>SQL Server Master Data Services (CTP 1.2)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>当实体事务日志类型设置为属性时，事务可能无法正常运行
**问题和对客户的影响：** 在 **中将实体事务日志类型设置为“属性”**[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] （默认值为“成员”） 时，以下方案会失败：

* 网站中不显示实体更改的事务。
* 无法打开网站上的“事务”  页并撤消事务。
* 在网站中，无法使用事务批注更新实体。

**解决方法：**没有解决方法。

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>将“仅复制提交的版本”  设置为 false 时，复制版本可能无法正常运行
-  **问题和对客户的影响：** 将“仅复制提交的版本”  设置设置为“否”  （默认值为“是” ）时，复制版本操作可能失败。 没有错误消息。
-  **解决方法：**没有解决方法。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-11-december--2016"></a>SQL Server vNext CTP 1.1（2016 年 12 月）
### <a name="supported-installation-scenarios-ctp-11"></a>支持的安装方案 (CTP 1.1)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 仅作为测试版本。  不支持生产部署。 建议在虚拟机上安装和测试 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 。

具体而言，虽然以下方案可能适用于你，但尚未完全通过测试且在 **中** 不 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]受支持：
- 卸载 CTP 1.1。
- 与任何其他版本的 SQL Server 并行安装。
- 从 SQL Server 早期版本升级。
- 没有作为 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 安装一部分的 SQL Server 功能包组件可用。

### <a name="documentation-ctp-11"></a>文档 (CTP 1.1)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过**适用于：**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

### <a name="sql-server-master-data-services-ctp-11"></a>SQL Server Master Data Services (CTP 1.1)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>当实体事务日志类型设置为属性时，事务可能无法正常运行
**问题和对客户的影响：** 在 **中将实体事务日志类型设置为“属性”**[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] （默认值为“成员”） 时，以下方案会失败：

* 网站中不显示实体更改的事务。
* 无法打开网站上的“事务”  页并撤消事务。
* 在网站中，无法使用事务批注更新实体。

**解决方法：**没有解决方法。

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>将“仅复制提交的版本”  设置为 false 时，复制版本可能无法正常运行
-  **问题和对客户的影响：** 将“仅复制提交的版本”  设置设置为“否”  （默认值为“是” ）时，复制版本操作可能失败。 没有错误消息。
-  **解决方法：**没有解决方法。

### <a name="sql-server-integration-services-ssis-ctp-11"></a>SQL Server Integration Services (SSIS) (CTP 1.1)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>如果安装了 SSIS Scale Out，删除 SSIS 目录可能会失败
**问题和对客户的影响**：如果计算机上安装了 SSIS Scale Out 功能，删除 SSISDB 目录数据库可能会失败，错误如下：“无法删除登录名‘login’  ，因为此用户当前已登录”。
   
**解决方法**：
-   在 Scale Out Master 计算机上，运行命令“services.msc”，打开“服务”窗口。 停止 SQL Server Integration Services Cluster Master 服务。
-   在连接到主服务器的 Scale Out Worker 计算机上，运行命令“services.msc”，打开“服务”窗口。 停止 SQL Server Integration Services Cluster Worker 服务。

现在可以删除 SSISDB 目录数据库。

#### <a name="odbc-components-are-not-supported-in-this-ctp-release"></a>此 CTP 版本不支持 ODBC 组件
**问题和对客户的影响**：此 CTP 版本不支持 ODBC 连接管理器、源和目标。

**解决方法：**没有解决方法。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-10-november-2016"></a>SQL Server vNext CTP 1.0（2016 年 11 月）
### <a name="supported-installation-scenarios-ctp10"></a>支持的安装方案 (CTP1.0)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 仅作为测试版本。  不支持生产部署。 建议在虚拟机上安装和测试 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 。

具体而言，虽然以下方案可能适用于你，但尚未完全通过测试且在 **中** 不 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]受支持：
- 卸载 CTP 1.0。
- 与任何其他版本的 SQL Server 并行安装。
- 从 SQL Server 早期版本升级。
- 没有作为 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 安装一部分的 SQL Server 功能包组件可用。

### <a name="documentation-ctp-10"></a>文档 (CTP 1.0)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过**适用于：**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

### <a name="sql-server-database-engine-ctp-10"></a>SQL Server 数据库引擎 (CTP 1.0)
-  **问题和对客户的影响：** CTP1 中的 `STRING_AGG` 函数返回作为结果的 LOB 类型（如 `NVARCHAR(MAX)`）。 在将来的 CTP 版本中，此行为可能改变且 `STRING_AGG` 可能返回 `NVARCHAR(4000)` （如果输入值不是 LOB 类型）。 如果串联结果无法适应 `NVARCHAR(4000)`，可能引发溢出错误。

-  **问题和对客户的影响：**避免将非保留关键字（如 `WITHIN`）作为 `STRING_AGG` 表达式的别名。 （例如 `SELECT Company.Name, STRING_AGG(Product.Name, ',') AS WITHIN FROM TableA;`。）在将来的 CTP 版本中，`STRING_AGG` 调用后的 `WITHIN` 令牌可用作 `STRING_AGG` 函数的一部分。

-  **解决方法：**避免使用 `WITHIN` 别名或添加 `AS WITHIN` 作为别名规范，以避免与可能添加到 `STRING_AGG` 函数的将来更改冲突。


### <a name="sql-server-integration-services-ctp-10"></a>SQL Server Integration Services (CTP 1.0)
#### <a name="stop-operation-in-ssis-catalog-may-fail"></a>SSIS 目录中的停止操作可能会失败
**问题和对客户的影响：**[!INCLUDE[ssIS_md](../includes/ssis-md.md)] 中使用 [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)] 或 catalog.stop_operation 存储过程的停止操作可能会失败，错误如下：执行用户定义的例程或聚合“stop_operation_internal”时发生 .NET Framework 错误。

-  **解决方法：**打开 Windows 任务管理器。 在“进程”  选项卡中，查找名为“ISServerExec”  的进程，单击“结束任务”  以结束进程。

#### <a name="create-dump-of-ssis-pacakge-execution-may-fail"></a>创建 SSIS 包执行的转储可能会失败
**问题和对客户的影响：** 使用 catalog.create_execution_dump 存储过程创建包执行的转储可能会失败，错误如下：执行用户定义例程或聚合“create_execution_dump_internal”时发生 .NET Framework 错误。

-  **解决方法：** 打开 Windows 任务管理器。 在“进程”  选项卡上，查找名为“ISServerExec” 的进程，右键单击此进程，然后单击“创建转储文件” 。

#### <a name="get-perf-counter-of-ssis-package-execution-may-fail"></a>获取 SSIS 包执行的性能计数器可能会失败
**问题和对客户的影响：** 使用表值函数 catalog.dm_execution_performance_counters 查询 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 性能计数器可能会失败，错误如下：执行用户定义例程或聚合“get_execution_perf_counters”时发生 .NET Framework 错误”。

-  **解决方法**：使用 Windows 性能监视器直接监视性能计数器值。 对于针对特定包执行的性能计数器，没有解决方法。

#### <a name="deleting-catalog-may-fail-when-ssis-scale-out-master-is-installed"></a>如果安装了 SSIS Scale Out Master，删除目录可能会失败
**问题和对客户的影响：** 如果计算机上安装了 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] Scale Out 功能，删除 **SSISDB** 目录可能会失败，错误如下：无法删除登录名“…”， ，因为此用户当前已登录”。 

**解决方法**： 
* 在 Scale Out Master 计算机上，运行命令“services.msc”，打开“服务”  窗口并停止“SQL Server Integration Services Cluster Master”  服务。 

* 在连接到主服务器的 Scale Out Worker 计算机上，运行命令“services.msc”，打开“服务”  窗口。 停止“SQL Server Integration Services Cluster Worker”  服务。 

现在应能够删除 **SSISDB** 目录。

#### <a name="odbc-connector-in-ssis-is-not-supported"></a>不支持 SSIS 中的 ODBC 连接器
-  **问题和对客户的影响：** 不支持 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 中的 ODCB 连接器。
-  **解决方法：** 没有解决方法。

### <a name="sql-server-reporting-services-ctp-10"></a>SQL Server Reporting Services (CTP 1.0)

SQL Server Reporting Services 不会发布 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]的任何新功能。

### <a name="sql-server-master-data-services-ctp-10"></a>SQL Server Master Data Services (CTP 1.0)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>当实体事务日志类型设置为属性时，事务可能无法正常运行
**问题和对客户的影响：** 在 **中将实体事务日志类型设置为“属性”**[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] （默认值为“成员”） 时，以下方案会失败：

* 网站中不显示实体更改的事务。
* 无法打开网站上的“事务”  页并撤消事务。
* 在网站中，无法使用事务批注更新实体。

**解决方法：**没有解决方法。

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>将“仅复制提交的版本”  设置为 false 时，复制版本可能无法正常运行
**问题和对客户的影响：** 将“仅复制提交的版本”  设置设置为“否”  （默认值为“是” ）时，复制版本操作可能失败。 没有错误消息。

**解决方法：**没有解决方法。
 
### <a name="sql-server-management-studio-ssms-ctp-10"></a>SQL Server Management Studio (SSMS) (CTP 1.0)
SQL Server Management Studio 需要单独下载。  有关最新信息，请参阅 [SQL Server Management Studio 发行说明](https://msdn.microsoft.com/library/mt238486.aspx)。

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 与 SQL Server 工程团队合作 
- [堆栈溢出（标记 sql-server）- 询问技术问题](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 论坛 - 询问技术问题](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 报告 bug 和请求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有关 R 的一般讨论](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)


