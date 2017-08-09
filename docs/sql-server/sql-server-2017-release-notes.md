---
title: "SQL Server 2017 发行说明 | Microsoft Docs"
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
ms.translationtype: HT
ms.sourcegitcommit: 6aa73e749d4f308265dfe27a160802c15a391a3e
ms.openlocfilehash: a2950b6aef0e12653efbb9eb26fd3f1ae6cb951e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-2017-release-notes"></a>SQL Server 2017 发行说明
本主题介绍 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]的限制和问题。 相关信息请参见以下内容：

- [SQL Server 2017 的新增功能](../sql-server/what-s-new-in-sql-server-2017.md)。
- [Linux 上的 SQL Server 发行说明](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes)的限制和问题。
- [SQL Server Reporting Services 发行说明](../reporting-services/reporting-services-release-notes.md)的限制和问题。

 **进行试用：**    
   -   [![从评估中心下载](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  从 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 评估中心 **[下载](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 候选发布（RC1 - 2017 年 7 月）

### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SQL Server Integration Services (SSIS)（RC1 - 2017 年 7 月）
- **问题和对客户的影响：**存储过程 [catalog].[create_execution] 的参数 runincluster 重命名为 runinscaleout，以保持一致性和可读性。
- **解决方法：**如果现有脚本在 Scale Out 中运行包，必须将参数名称从 runincluster 更改为 runinscaleout，以使脚本在 RC1 中正常运行。

- **问题和对客户的影响：**SQL Server Management Studio (SSMS) 17.1 及更早版本无法在 RC1 的 Scale Out 中触发包执行。 错误消息为：“@runincluster 不是过程 create_execution 的参数。” SSMS 的下一个版本，即版本 17.2 中修复了此问题。 SSMS 的版本 17.2 及更高版本支持 Scale Out 中的新参数名称和包执行。 
- **解决方法：**SSMS 版本 17.2 可用之前，可以使用 SSMS 的现有版本生成包执行脚本，然后在脚本中将 runincluster 参数的名称更改为 runinscaleout，并运行该脚本。

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1（2017 年 5 月）
### <a name="documentation-ctp-21"></a>文档 (CTP 2.1)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过 **适用于**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **问题和对客户的影响：**如果同一计算机同时具有 SQL Server Reporting Services 和 Power BI 报表服务器，但卸载了其中之一，则不可再通过报表服务器配置管理器连接到其余的报表服务器。
- **解决方法**：要解决此问题，必须在卸载其中一个服务器后执行以下操作。

    1. 在管理员模式下启动命令提示符。
    2. 转到安装其余报表服务器的目录。

        Power BI 报表服务器的默认位置：C:\Program Files\Microsoft Power BI Report Server

        SQL Server Reporting Services 的默认位置：C:\Program Files\Microsoft SQL Server Reporting Services

    3. 然后转到下一个文件夹。 可以是 SSRS 或 PBIRS，具体取决于剩余内容。
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

- **问题和对客户的影响：**在已安装 2016 版 TSqlLanguageService.msi 的计算机上安装（通过 SQL 安装程序或作为独立可再发行组件安装）后，系统将删除 v13.* (SQL 2016) 版 Microsoft.SqlServer.Management.SqlParser.dll 和 Microsoft.SqlServer.Management.SystemMetadataProvider.dll。 在这些程序集的 2016 版本上具有依赖项的应用程序都会停止工作，出现如下错误：错误: 无法加载文件或程序集“Microsoft.SqlServer.Management.SqlParser，版本=13.0.0.0，区域性=中性，PublicKeyToken=89845dcd8080cc91”或其某个依赖项。系统找不到指定文件。

   此外，尝试重装 2016 版 TSqlLanguageService.msi 的操作都将失败，并显示消息：安装 Microsoft SQL Server 2016 T-SQL 语言服务失败，因为计算机上已存在更高版本。

- **解决方法**：要解决此问题并修复依赖于 v13 版程序集的应用程序，请执行下列步骤：

   1. 转到“添加/删除程序”
   1. 找到 Microsoft SQL Server vNext T-SQL 语言服务 CTP2.1，右键单击它，然后选择“卸载”。
   1. 删除该组件后，即可修复已损坏的应用程序（或重新安装适当版本的 TSqlLanguageService.MSI）

   此解决方法将删除这些程序集的 v14 版本，因此任何依赖于 v14 版本的应用程序将不再运行。 如果需要这些程序集，则需单独安装，无需并行安装任何 2016 版。

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0（2017 年 4 月）
### <a name="documentation-ctp-20"></a>文档 (CTP 2.0)
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文档集中。  特定于 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文章内容将通过 **适用于**标注。 
- **问题和对客户的影响：**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 没有可用的脱机内容。

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性组

- **问题和对客户的影响：**如果 SQL Server 主版本低于托管主要副本的实例，托管可用性组次要副本的 SQL Server 实例将崩溃。 如果从托管可用性组且受支持的任意 SQL Server 版本升级到 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0，则这些升级将受到影响。 以下步骤会导致此情况。 

> 1. 用户根据[最佳做法](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)升级托管次要副本的 SQL Server 实例。
> 2. 升级后，会发生故障转移，并且在完成可用性组中所有次要副本的升级之前，刚升级的次要副本将变为主要副本。 旧的主要副本现在是次要副本，即版本低于主要副本。
> 3. 可用性组的配置不受支持，且其余所有次要副本都可能很容易崩溃。 

- **解决方法**：连接到托管新的主要副本的 SQL Server 实例并从配置中删除有问题的次要副本。

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   托管次要副本的 SQL Server 实例即可恢复。

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 与 SQL Server 工程团队合作 
- [堆栈溢出（标记 sql-server）- 询问技术问题](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 论坛 - 询问技术问题](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 报告 bug 和请求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有关 R 的一般讨论](https://www.reddit.com/r/SQLServer/)

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
