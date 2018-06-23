---
title: 创建报表服务器数据库（SSRS 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], databases
- report server database
- databases [Reporting Services], creating
ms.assetid: 8a3a6ffe-4001-46be-8548-94532550f6a5
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 5cd23aaa93b60a2af7212ca8c98025a51f92d4c6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018793"
---
# <a name="create-a-report-server-database--ssrs-configuration-manager"></a>创建报表服务器数据库（SSRS 配置管理器）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **本机模式** 使用两个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据库存储报表服务器元数据和对象。 一个数据库用于主存储，另一个数据库用于存储临时数据。 这两个数据库一起创建，并按名称绑定。 通过默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，将这两个数据库命名为 `reportserver` 和 `reportservertempdb`。 这两个数据库统称为“报表服务器数据库”或“报表服务器目录”。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **SharePoint 模式** 包含用于数据警报元数据的第三个数据库。 为每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序创建三个数据库，默认情况下，这些数据库名称包含表示服务应用程序的 guid。 以下是三个 SharePoint 模式数据库的示例名称：  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  
  
> [!IMPORTANT]  
>  请不要编写对报表服务器数据库运行查询的应用程序。 报表服务器数据库不是公用架构。 从一个版本升级到下一个版本时可能会更改表结构。 如果编写一个需要访问报表服务器数据库的应用程序，则始终使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API 来访问报表服务器数据库。  
>   
>  唯一的例外是执行日志视图。 有关详细信息，请参阅[报表服务器执行日志和 ExecutionLog3 视图](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
## <a name="ways-to-create-the-report-server-database"></a>创建报表服务器数据库的方式  
 **本机模式：** 您可以通过以下方式创建本机模式的报表服务器数据库：  
  
-   自动：如果选择默认配置安装选项，请使用 SQL Server 安装向导。 在 SQL Server 安装向导中，这是“报表服务器安装选项”页中的 **“安装和配置”** 。 如果选择 **“仅安装”** 选项，则必须使用 Reporting Services 配置管理器来创建数据库。  
  
-   手动：使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器。 如果使用远程 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 来承载该数据库，则必须手动创建报表服务器数据库。 有关详细信息，请参阅[创建本机模式报表服务器数据库（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。  
  
 **SharePoint 模式：** “报表服务器安装选项”页中只有一个用于 SharePoint 模式的选项 **“仅安装”**。 此选项安装所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共享服务。 下一步是通过以下方式之一至少创建一个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序：  
  
-   使用 SharePoint 管理中心创建 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。 有关详细信息，请参阅的"服务应用程序"部分[步骤 3： 创建 Reporting Services 服务应用程序](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md#bkmk_create_serrviceapplication)。  
  
-   使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] PowerShell cmdlet 创建服务应用程序和报表服务器数据库。 有关详细信息，请参阅用于创建服务应用程序主题中的示例[Reporting Services SharePoint 模式的 PowerShell cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)。  
  
## <a name="database-server-version-requirements"></a>数据库服务器版本要求  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用来承载报表服务器数据库。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例可以是本地或远程实例。 以下是可用于承载报表服务器数据库的支持的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 版本：  
  
- SQL Server 2014
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
 若要在远程计算机上创建报表服务器数据库，则需要将连接配置为使用域用户帐户或具有网络访问权限的服务帐户。 如果决定使用远程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，请仔细考虑报表服务器应使用哪些凭据来连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 有关详细信息，请参阅[配置报表服务器数据库连接（SSRS 配置管理器）](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
> [!IMPORTANT]  
>  报表服务器和用于承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例可位于不同的域中。 对于 Internet 部署，通常的做法是使用防火墙后的服务器。 如果要配置用于 Internet 访问的报表服务器，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 凭据连接到位于防火墙后的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例并使用 IPSEC 保护连接的安全。  
  
## <a name="database-server-edition-requirements"></a>数据库服务器版本类别要求  
 创建报表服务器数据库时，请注意并非所有版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 均可用来承载数据库。 有关详细信息，请参阅的"报表服务器数据库服务器版本要求"部分[支持的 SQL Server 2014 的版本功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 配置管理器&#40;del&#41;](/sql/2014/sql-server/install/reporting-services-configuration-manager-native-mode)  
  
  
