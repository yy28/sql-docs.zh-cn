---
title: "什么 &#39; s 在 SQL Server 自 2017 年中的 Integration Services 中的新增功能 |Microsoft 文档"
ms.custom: 
ms.date: 09/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: 63aba0f64bc63a3a86e5aa07245375938acdf6e4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/29/2017

---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>什么 &#39; s 在 SQL Server 自 2017 年中的 Integration Services 中的新增功能
本主题介绍 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中新增或更新的功能。

>   [!NOTE]
> SQL Server 2017 还包括 SQL Server 2016 的功能以及 SQL Server 2016 更新中新增的功能。 若要了解 SQL Server 2016 中的新 SSIS 功能，请参阅 [SQL Server 2016 Integration Services 中的新增功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)。

## <a name="highlights-of-this-release"></a>此版本的要点

以下是 SQL Server 自 2017 年中的 Integration Services 的最重要新功能。

-   **向外扩展**。将 SSIS 包执行更轻松地分配给多个辅助计算机，和从一台主计算机管理执行和辅助角色。 有关详细信息，请参阅[集成服务向外扩展](../integration-services/scale-out/integration-services-ssis-scale-out.md)。

-   **在 Linux 上的 integration Services**。 在 Linux 计算机上运行 SSIS 包。 有关详细信息，请参阅[提取、 转换和加载数据使用 SSIS 的 Linux 上](../linux/sql-server-linux-migrate-ssis.md)。

-   **连接改进**。 连接到的 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online OData 数据源与更新的 OData 组件。 

## <a name="new-in-azure-data-factory"></a>Azure 数据工厂中的新增功能

使用 Azure 数据工厂中自 2017 年 9 月版本 2 公共预览版，你现在可以执行以下操作：
-   将包部署到 Azure SQL 数据库上的 SSIS 目录数据库 (SSISDB)。
-   运行部署到 Azure SSIS 集成运行库的 Azure 数据工厂版本 2 的组件上的 Azure 包。

有关详细信息，请参阅[到云中的 SQL Server Integration Services 工作负荷提供提起并移动](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

这些新功能需要 SQL Server Data Tools (SSDT) 版本 17.2 或更高版本，但不是需要 SQL Server 2017 或 SQL Server 2016。 当将包部署到 Azure 时，包部署向导始终的包升级到最新的包格式。

## <a name="new-in-the-azure-feature-pack"></a>Azure 功能包中的新增功能

除了 SQL Server 中的连接改进，用于 Azure 的 Integration Services 功能包添加了对 Azure 数据湖存储支持。 有关详细信息，请参阅博客文章[新 Azure 功能包版本增强 ADLS 连接](https://blogs.msdn.microsoft.com/ssis/2017/08/29/new-azure-feature-pack-release-strengthening-adls-connectivity/)。 另请参阅[Azure Feature Pack 为 Integration Services (SSIS)](azure-feature-pack-for-integration-services-ssis.md)。

## <a name="new-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) 中的新增功能

现在，你可以开发 SSIS 项目和面向通过 2017 在 Visual Studio 2017 或 Visual Studio 2015 中的 SQL Server 版本 2012年的包。 有关详细信息，请参阅[下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)。

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>在 SQL Server 自 2017 年 1 RC1 SSIS 中的新增功能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>在向外扩展 for SSIS 的新功能和更改功能

-   Scale Out 主要角色现在支持高可用性。 你可以启用 Always On ssisdb 和设置 Windows Server 故障转移为服务器群集承载缩放出主机服务。 通过将此更改应用于出母版缩放，避免单点故障，并为整个向外扩展部署中提供高可用性。
-   改进了 Scale Out 辅助角色中执行日志的故障转移处理。 执行日志保存到本地磁盘中，以防缩放出工作进程意外停止。 更高版本，辅助角色重新启动时，它将重新加载持久化的日志，并继续将它们保存到 SSISDB。
-   存储过程 [catalog].[create_execution] 的参数 runincluster 重命名为 runinscaleout，以保持一致性和可读性。 此更改参数名称产生下列影响：
    -   如果你有现有的脚本以在向外扩展运行包，则必须更改中的参数名称*runincluster*到*runinscaleout*若要使脚本在 RC1 中工作。
    -   SQL Server Management Studio (SSMS) 17.1 和更早版本，无法触发中向外扩展 RC1 中的包执行。 错误消息为：“@runincluster 不是过程 create_execution 的参数。” SSMS 的下一个版本，即版本 17.2 中修复了此问题。 版本 17.2 及更高版本的 SSMS 中向外扩展支持新的参数名称和包执行。SSMS 版本 17.2 可用，一种解决方法之前，你可以使用现有版本的 SSMS 生成包执行脚本，然后更改的名称*runincluster*参数*runinscaleout*脚本，并运行的脚本中。
-   SSIS 目录具有新的全局属性，用于指定执行 SSIS 包的默认模式。 在调用时应用此新属性**[目录]。 [create_execution]**存储过程，并*runinscaleout*参数设置为 null。 此模式也适用于 SSIS SQL 代理作业。 你可以在 SSMS 中，或使用以下命令的 SSISDB 节点的属性对话框中设置新的全局属性：
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>SQL Server 2017 CTP 2.1 中新的 SSIS 功能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>在向外扩展 for SSIS 的新功能和更改功能

-   你现在可以使用**Use32BitRuntime**参数时触发执行中向外扩展。
-   Scale Out 中用于包执行的 SSISDB 日志记录性能得到了改进。 事件消息和消息上下文日志现批量写入 SSISDB 中，而不是逐一写入。 以下是有关此改进的一些其他说明：        
    - 在当前版本的 SQL Server Management Studio (SSMS) 中，某些报表目前不显示要在 Scale Out 中执行的日志。预计将在下一版本的 SSMS 中支持它们。 受影响的报表包括*所有连接*报表，*错误上下文*报表，与*连接信息*的集成服务仪表板的部分。
    - 新建一列**event_message_guid**已添加。 使用此列联接 [目录]。视图 [event_message_context] 和 [目录]。[event_messages] 查看而不是使用**event_message_id**在查询中向外扩展执行这些日志。
-   若要获取用于 SSIS 向外扩展，管理应用程序[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.1 或更高版本。

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>在 SQL Server 自 2017 年 1 CTP 2.0 中的 SSIS 中的新增功能

在 SQL Server 自 2017 年 1 CTP 2.0 中没有新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>在 SQL Server 自 2017 年 1 CTP 1.4 中的 SSIS 中的新增功能

在 SQL Server 自 2017 年 1 CTP 1.4 中没有新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>在 SQL Server 自 2017 年 1 CTP 1.3 SSIS 中的新增功能

SQL Server 自 2017 年 1 CTP 1.3 中有任何新的 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>在 SQL Server 自 2017 年 1 CTP 1.2 SSIS 中的新增功能

SQL Server 自 2017 年 1 CTP 1.2 中没有新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>在 SQL Server 自 2017 年 1 CTP 1.1 中的 SSIS 中的新增功能

SQL Server 自 2017 年 1 CTP 1.1 中没有新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>SQL Server 2017 CTP 1.0 中新的 SSIS 功能

### <a name="scale-out-for-ssis"></a>SSIS 的 Scale Out

Scale Out 功能使在多台计算机上运行 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 变得更加简单。 
   
安装 Scale Out Master 和 Worker 之后，可分发包以在不同的 Worker 上自动执行。 如果执行意外终止，将自动重试该执行。 此外，可使用 Master 集中管理所有执行和 Worker。
   
有关详细信息，请参阅 [Integration Services Scale Out](../integration-services/scale-out/integration-services-ssis-scale-out.md)。
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>支持 Microsoft Dynamics Online 资源

OData 源和 OData 连接管理器现支持连接到 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 的 OData 源。


