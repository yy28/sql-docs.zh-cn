---
title: 创建本机模式报表服务器数据库（SSRS 配置管理器）| Microsoft Docs
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
- databases [Reporting Services], creating
ms.assetid: 81b9f4ad-800b-4688-8b47-a5a83dc8ff10
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 2690d8684bd244ecc671168d9648832a5a2ca9eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123833"
---
# <a name="create-a-native-mode-report-server-database--ssrs-configuration-manager"></a>创建本机模式报表服务器数据库（SSRS 配置管理器）
  本机模式的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库用于内部存储。 该数据库是必需的，它用于存储已发布的报表、模型、共享数据源、会话数据、资源和服务器元数据。  
  
 若要创建报表服务器数据库或更改连接字符串或凭据，请使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器的“数据库”页中的选项。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|  
  
## <a name="when-to-create-or-configure-the-report-server-databases"></a>何时创建或配置报表服务器数据库  
 如果在“仅文件”模式下安装报表服务器，则必须创建和配置报表服务器数据库。  
  
 如果你安装[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在默认配置为纯模式，报表服务器数据库创建和自动配置的报表服务器实例的安装。 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器查看或修改安装程序为您配置的设置。  
  
##  <a name="rsdbrequirements"></a> 开始之前  
 创建或配置报表服务器数据库是一个多步骤过程。 创建报表服务器数据库之前，请考虑要如何指定下列各项：  
  
 选择数据库服务器  
 查看支持的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 版本，以及主题[创建报表服务器数据库（SSRS 配置管理器）](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)中支持的版本。  
  
 启用 TCP/IP 连接  
 启用 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的 TCP/IP 连接。 默认情况下，某些 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 版本不启用 TCP/IP。 本主题中提供了相关说明。  
  
 打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的端口  
 对于远程服务器，如果使用的是防火墙软件，则必须打开 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 侦听的端口。  
  
 确定报表服务器凭据  
 确定报表服务器与报表服务器数据库的连接方式。 凭据类型包括域用户帐户、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库用户帐户或报表服务器服务帐户。  
  
 这些凭据经过加密并存储在 RSReportServer.config 文件中。 报表服务器将这些凭据用于与报表服务器数据库进行的连接。 如果您要使用 Windows 用户帐户或数据库用户帐户，请确保指定已经存在的帐户。 尽管 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器将创建登录名并设置必要的权限，但不会为您创建帐户。 有关详细信息，请参阅[配置报表服务器数据库连接（SSRS 配置管理器）](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
 确定报表服务器语言  
 选择要为报表服务器指定的语言。 当用户使用不同语言版本的浏览器连接到服务器时，预定义的角色名称、说明和“我的报表”文件夹不会以不同的语言显示。  
  
 检查凭据以创建和设置数据库  
 确保您拥有的帐户凭据具有在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例上创建数据库的权限。 这些凭据用于一次性连接以创建报表服务器数据库和 **RSExecRole**。 如果登录名尚不存在，将为报表服务器所用的帐户创建一个数据库用户登录名以连接到该数据库。 您可以用您登录时所用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户进行连接，也可以输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库登录名。  
  
### <a name="to-enable-access-to-a-remote-report-server-database"></a>启用对远程报表服务器数据库的访问  
  
1.  如果您使用的是远程 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，请登录到此数据库服务器以验证或启用 TCP/IP 连接。  
  
2.  依次指向 **“开始”**、 **“所有程序”**、 **Microsoft SQL Server**、 **“配置工具”**，再单击 **“SQL Server 配置管理器”**。  
  
3.  打开 **“SQL Server 网络配置”**。  
  
4.  选择实例。  
  
5.  右键单击**TCP/IP**单击**已启用**。  
  
6.  重新启动服务。  
  
7.  打开防火墙软件并打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 侦听的端口。 对于默认实例，此端口通常为用于 TCP/IP 连接的 1433 端口。 有关详细信息，请参阅 [联机丛书中的](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) 为数据库引擎访问配置 Windows 防火墙 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="to-create-a-local-report-server-database"></a>创建本地报表服务器数据库  
  
1.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器并连接到要为其创建数据库的报表服务器实例。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
2.  在“数据库”页上，单击 **“更改数据库”**。  
  
3.  单击 **“创建新的报表服务器数据库”**，然后单击 **“下一步”**。  
  
4.  连接到您将用于创建和承载报表服务器数据库的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例：  
  
    1.  键入要使用的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例。 向导将显示作为默认实例（如果可用）运行的本地 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 否则，您必须键入要使用的服务器和实例。 以此种格式指定命名的实例：\<servername>\\<instancename\>。  
  
    2.  输入用于一次性连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的凭据以创建报表服务器数据库。 有关如何使用这些凭据的详细信息，请参阅本主题中的 [开始之前](#rsdbrequirements) 。  
  
    3.  单击 **“测试连接”** 以验证与服务器的连接。  
  
    4.  单击“下一步” 。  
  
5.  指定用于创建数据库的属性。 有关如何使用这些属性的详细信息，请参阅本主题中的 [开始之前](#rsdbrequirements) ：  
  
    1.  键入报表服务器数据库的名称。 创建主数据库时，会同时为其创建一个临时数据库。 请考虑使用一个说明性名称来帮助记忆数据库的使用方式。 请注意，您指定的名称将在数据库的生存期内使用。 在创建报表服务器数据库之后，不能对其进行重命名。  
  
    2.  选择要显示角色定义和“我的报表”所用的语言。  
  
    3.  报表服务器模式始终设置为 **“本机”**。  
  
    4.  单击“下一步” 。  
  
6.  指定报表服务器用来连接到报表服务器数据库的凭据。  
  
    1.  指定身份验证类型：  
  
         选择 **“数据库凭据”** 以使用已定义的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库登录名进行连接。 如果报表服务器位于不同域、不可信域或装有防火墙的计算机中，则建议使用数据库凭据。  
  
         如果你拥有的最低特权域用户帐户具有登录到该计算机和数据库服务器的权限，请选择“Windows 凭据”。  
  
         如果希望报表服务器使用其自身的服务帐户进行连接，则选择 **“服务凭据”** 。 使用此选项，该服务器将使用集成安全性进行连接；凭据不进行加密或存储。  
  
    2.  单击“下一步” 。  
  
7.  检查“摘要”页上的信息以确保设置正确，然后单击 **“下一步”**。  
  
8.  单击“报表服务器 URL”页或“报表管理器 URL”页上的 URL，验证连接。 必须定义这些 URL 才能进行此测试。 如果报表服务器数据库连接有效，您会在浏览器窗口中看到报表服务器文件夹层次结构或报表管理器。 有关详细信息，请参阅[验证 Reporting Services 安装](verify-a-reporting-services-installation.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [配置报表服务器数据库连接&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [数据库&#40;SSRS 本机模式&#41;](../../sql-server/install/database-ssrs-native-mode.md)   
 [管理 Reporting Services 本机模式报表服务器](../report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  