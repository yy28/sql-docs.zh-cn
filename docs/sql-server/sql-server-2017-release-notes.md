---
title: "SQL Server 自 2017 年 1 发行说明 |Microsoft 文档"
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-server-2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 67c1c0f3a9da6cc5d050da5db8a493f5da934c2a
ms.openlocfilehash: fa45fea4ebb378f035b4b4af2b1fa8a20bc152a5
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-2017-release-notes"></a>SQL Server 2017 发行说明
本主题介绍 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的限制和问题。 有关相关信息，请参阅以下：

- [SQL Server 自 2017 年中的新增](../sql-server/what-s-new-in-sql-server-2017.md)。
- [SQL Server 上 Linux 发行说明](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes)。
- [SQL Server Reporting Services 发行说明](../reporting-services/reporting-services-release-notes.md)。

 **进行试用：**    
   -   [![从评估中心下载](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  从 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 评估中心 **[下载](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 自 2017 年 1 CTP 2.1 (2017 年 5 月)
### <a name="documentation-ctp-21"></a>文档 (CTP 2.1)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过**适用于**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **问题及其对客户的影响：**如果你有 SQL Server Reporting Services 和 Power BI 报表服务器在同一计算机，并且卸载其中之一，你将不再能够连接到剩余的报表服务器与报表服务器配置管理器中。
- **解决方法**若要解决此问题，你必须卸载服务器之一后执行以下操作。

    1. 在管理员模式下启动命令提示符。
    2. 转到安装其余报表服务器的目录。

        *Power BI 报表服务器的默认位置： C:\Program Files\Microsoft Power BI 报表服务器*

        *SQL Server Reporting Services 的默认位置： C:\Program Files\Microsoft SQL Server Reporting Services*

    3. 然后转到下一个文件夹。 该地址可以是*SSRS*或*PBIRS*具体取决于什么剩余。
    4. 转到 WMI 文件夹。
    5. 运行以下命令：

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        如果看到它，可忽略以下错误。

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **问题及其对客户的影响：**后具有 2016年版本的计算机上安装*TSqlLanguageService.msi* v13.* (SQL 2016) 版本的安装 （通过 SQL 安装程序或作为独立的可再发行组件） *Microsoft.SqlServer.Management.SqlParser.dll*和*Microsoft.SqlServer.Management.SystemMetadataProvider.dll*会删除。 任何应用程序依赖于这些程序集的 2016年版本将然后停止正常运行，提供如下错误：*错误： 无法加载文件或程序集 Microsoft.SqlServer.Management.SqlParser，Version = 13.0.0.0，区域性 = neutral，PublicKeyToken = 89845dcd8080cc91 或其依赖项之一。系统找不到指定的文件。*

   此外，尝试重新安装 TSqlLanguageService.msi 的 2016年版本将失败并显示消息：*安装的 Microsoft SQL Server 2016 T-SQL 语言服务失败，因为计算机上已经存在的更高版本*。

- **解决方法**若要解决此问题并修复的应用程序依赖于 v13 程序集版本，请按照下列步骤：

   1. 转到**添加/删除程序**
   1. 查找*Microsoft SQL Server vNext T-SQL 语言服务 CTP2.1*，右键单击它，然后选择**卸载**。
   1. 删除该组件后，修复的应用程序已中断 (或重新安装相应版本的*TSqlLanguageService.MSI*)

   此解决方法将删除这些程序集的 v14 版本，因此任何依赖于 v14 版本的应用程序将不再运行。 如果需要这些程序集，则需单独安装，无需并行安装任何 2016 版。

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 自 2017 年 1 CTP 2.0 (自 2017 年 4 月)
### <a name="documentation-ctp-20"></a>文档 (CTP 2.0)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过**适用于**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性组

- **问题及其对客户的影响：**承载可用性组辅助副本的 SQL Server 实例崩溃，如果 SQL Server 主要版本低于承载主副本的实例。 影响从所有受支持版本的 SQL Server 承载可用性组迁移到 SQL Server 升级[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]CTP 2.0。 以下步骤会导致此情况。 

> 1. 用户升级中根据所使用的 SQL Server 实例承载辅助副本[最佳实践](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)。
> 2. 升级后，发生故障转移，并在完成升级的所有辅助副本的可用性组之前，新升级的辅助数据库将变成主。 旧的主要副本现在是次要副本，即版本低于主要副本。
> 3. 可用性组的配置不受支持，且其余所有次要副本都可能很容易崩溃。 

- **解决方法**连接到承载新的主副本和删除从配置有问题的辅助副本的 SQL Server 实例。

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   托管次要副本的 SQL Server 实例即可恢复。


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-14-march--2017"></a>SQL Server 自 2017 年 1 CTP 1.4 (自 2017 年 3 月)

### <a name="documentation-ctp-14"></a>文档 (CTP 1.4)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过**适用于**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-13-february--2017"></a>SQL Server 自 2017 年 1 CTP 1.3 (自 2017 年 2 月)
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

## <a name="sql-server-2017-ctp-12-january--2017"></a>SQL Server 自 2017 年 1 CTP 1.2 (2017 年 1 月)
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

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 与 SQL Server 工程团队合作 
- [堆栈溢出（标记 sql-server）- 询问技术问题](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 论坛 - 询问技术问题](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 报告 bug 和请求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有关 R 的一般讨论](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)


