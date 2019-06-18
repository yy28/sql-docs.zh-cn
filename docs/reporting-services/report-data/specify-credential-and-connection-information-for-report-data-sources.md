---
title: 为报表数据源指定凭据和连接信息 | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- Windows authentication [Reporting Services]
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- unattended report processing [Reporting Services]
- reports [Reporting Services], security
- remote data sources [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- prompted credentials [Reporting Services]
- multiple connections
- stored credentials [Reporting Services]
- security [Reporting Services], data sources
- Windows integrated security [Reporting Services]
ms.assetid: fee1a663-a313-424a-aed2-5082bfd114b3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d6b5041b07551ba8bbd23cc3f737fc0c09d72ff1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575342"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>为报表数据源指定凭据和连接信息
  报表服务器可以使用凭据连接到向报表提供内容或者向数据驱动订阅提供收件人信息的外部数据源。 您可以指定凭据使用 Windows 身份验证、数据库身份验证、自定义身份验证或不使用任何身份验证。 当通过网络发送连接请求时，报表服务器便会模拟用户帐户或无人参与的执行帐户。 有关建立连接请求时所处安全上下文的详细信息，请进一步参阅本主题中的 [数据源配置和网络连接](#DataSourceConfigurationConnections) 。  
  
> [!NOTE]  
>  凭据也可以用于对访问报表服务器的用户进行身份验证。 有关向报表服务器验证用户身份的信息将在其他主题中介绍。  
  
 与外部数据源的连接是在创建报表时定义的。 发布报表后可以单独管理该连接。 可以指定静态连接字符串或表达式，这允许用户从动态列表中选择数据源。 有关如何指定数据源类型和连接字符串的详细信息，请参阅 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
## <a name="when-credentials-are-used-in-report-builder"></a>在报表生成器中使用凭据时  
 在报表生成器中，在连接到报表服务器或完成数据相关的任务时（例如，创建嵌入数据源，运行数据集查询或预览报表）通常会使用凭据。 凭据不保存在报表中。 将在报表服务器或本地客户端对凭据进行单独管理。 下表介绍了可能需要提供的凭据类型、凭据的存储位置以及使用方法：  
  
-   在“Reporting Services 登录”对话框中输入的报表服务器凭据。  
  
     当您首次保存到、发布到或浏览到报表服务器或 SharePoint 站点时，可能需要输入凭据。 在报表生成器会话结束之前，将始终使用所输入的凭据。 如果选择保存凭据，则这些凭据将安全地与您的用户设置一起存储在您的计算机上。 在后续的报表生成器会话中，将使用保存的凭据连接到同一报表服务器或 SharePoint 站点。 报表服务器管理员或 SharePoint 管理员指定要使用哪一种类型的凭据。  
  
-   在嵌入数据源的[“数据源属性”对话框 ->“凭据”（报表生成器）](https://msdn.microsoft.com/library/4531f09f-d653-4c05-a120-d7788838bc99)页输入的数据源凭据。  
  
     报表服务器使用这些凭据与外部数据源建立数据连接。 对于某些类型的数据源，可以将凭据安全地存储在报表服务器上。 利用这些凭据，其他用户无需提供凭据即可运行报表进行基础数据连接。  
  
-   运行数据集查询、刷新数据集字段或预览报表时，在“输入数据源凭据”对话框中输入的数据源凭据  。  
  
     使用这些凭据，报表生成器可以与外部数据源建立数据连接，或对配置为提示需要提供凭据的报表进行预览。 在此对话框中输入的凭据不会存储在报表服务器中，且不能由其他用户使用。 在报表编辑会话期间，报表生成器会对这些凭据进行缓存，以便您无需在每次运行查询或预览报表时输入凭据。  
  
     对于共享数据源，使用 **“保存我的密码”** 选项可以将凭据与用户设置一起保存到本地计算机上。 报表生成器在每次连接到相应的外部数据源时使用保存的凭据。  
  
 有关详细信息，请参阅[“数据源属性”对话框 ->“常规”（报表生成器）](https://msdn.microsoft.com/library/b956f43a-8426-4679-acc1-00f405d5ff5b)和[在报表生成器中预览报表](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)。  
  
## <a name="using-remote-data-sources"></a>使用远程数据源  
 如果报表从远程数据库服务器检索数据，请验证以下内容：  
  
-   提供给数据库服务器的凭据有效。 如果使用的是 Windows 用户凭据，请确保用户拥有访问服务器和数据库的权限。  
  
-   数据库服务器使用的端口处于打开状态。 如果要访问外部计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据库，或者如果报表服务器数据库在外部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上，则必须在外部计算机上打开端口 1433 和 1434。 打开端口后务必重新启动服务器。 有关详细信息，请参阅 [为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。  
  
-   必须启用远程连接。 如果要访问外部计算机上的 SQL Server 关系数据库，则可以使用 SQL Server 配置管理器工具来验证是否启用了通过 TCP 的远程连接。  
  
## <a name="ways-to-specify-credentials-for-connecting-to-remote-data-sources"></a>指定用于连接到远程数据源的凭据的方法  
 向报表提供内容的数据源通常驻留在远程服务器上。 若要检索报表数据，报表服务器必须使用一组事先提供或在运行时获取的凭据连接到服务器。 配置数据源时，您可以按下列方式指定凭据：  
  
-   提示用户输入凭据。  
  
-   存储凭据。  
  
-   使用 Windows 集成安全性。  
  
-   不使用凭据。  
  
 网络环境决定了您可以支持的连接种类。 例如，如果启用了 Kerberos 版本 5 协议，则可以使用 Windows 身份验证中的委托功能和模拟功能来支持跨多个服务器的连接。 如果您的网络不支持这些安全功能，则需要针对连接约束采取相应的措施。 如果未启用委托和模拟，则在 Windows 凭据过期之前，可以跨一个计算机连接传递该凭据。 从客户端计算机到报表服务器计算机的用户连接可算作第一个连接。 如果该用户打开一个从远程服务器检索数据的报表，则该登录将计为第二个连接。如果此时指定了使用集成安全性的连接而未启用委托，则该登录将失败。  
  
 如果需要用多个连接来完成从客户端计算机到外部报表数据源的往返，请在以下策略中进行选择来建立多个连接：  
  
-   在域中启用模拟功能和委托功能，以便凭据可以不受限制地委托给其他计算机。  
  
-   使用已存储凭据或提示的凭据来查询报表数据的外部数据源。 凭据可以是 Windows 域帐户，也可以是数据库登录名。  
  
### <a name="prompted-credentials"></a>提示的凭据  
 将报表数据源连接配置为使用提示的凭据时，访问该报表的每个用户都必须输入用户名和密码才能检索数据。 建议将此方法用于包含机密数据的报表。 只能对按需运行的报表使用提示的凭据。 提示的凭据可以是 Windows 域帐户，也可以是数据库登录名。 若要使用 Windows 身份验证，则必须选择 **“在与数据源建立连接时用作 Windows 凭据”** 。 否则，报表服务器会将凭据传递给数据库服务器进行用户身份验证。 如果数据库服务器无法对您所提供的凭据进行身份验证，则该连接将失败。  
  
### <a name="windows-integrated-security"></a>Windows 集成安全性  
 使用 **“Windows 集成安全性”** 选项时，报表服务器会将访问报表的用户的安全令牌传递给外部数据源所在的服务器。 在这种情况下，系统不会提示用户键入用户名或密码。 如果启用了模拟功能和代理功能，建议使用此方法。 如果未启用这些功能，则只能在所有要访问的服务器都位于同一个计算机上时才能使用此方法。  
  
### <a name="stored-credentials"></a>存储的凭据  
 您可以存储用于访问外部数据源的凭据。 凭据以逆加密的形式存储在报表服务器数据库中。 您可以为报表中使用的每个数据源都指定同一套已存储凭据。 所提供的凭据会为每位运行该报表的用户检索相同的数据。  
  
 建议将已存储凭据作为远程数据库服务器访问策略的一部分。 如果要支持订阅，或计划生成报表历史记录或刷新报表快照的时间，则要求使用已存储凭据。 当报表作为后台进程运行时，报表服务器便会充当执行报表的代理。 此时，由于不存在用户上下文，报表服务器必须从报表服务器数据库获取凭据信息才能连接到数据源。  
  
 您指定的用户名和密码可以是 Windows 凭据，也可以是数据库登录名。 如果指定 Windows 凭据，报表服务器会将凭据传递给 Windows，用于随后的身份验证。 否则，凭据将传递给数据库服务器进行身份验证。  
  
#### <a name="how-to-grant-allow-log-on-locally-permissions-to-domain-user-accounts"></a>如何对域用户帐户授予“允许在本地登录”权限  
 如果使用已存储凭据连接到外部数据源，则 Windows 域用户帐户必须拥有在本地登录的权限。 此权限允许报表服务器模拟报表服务器上的用户，然后以该模拟用户的身份向外部数据源发送请求。  
  
 若要授予此权限，请执行以下操作：  
  
1.  在报表服务器计算机上的 **“管理工具”** 中，打开 **“本地安全策略”** 。  
  
2.  在 **“安全设置”** 下，展开 **“本地策略”** ，然后单击 **“用户权限分配”** 。  
  
3.  在详细信息窗格中，右键单击“允许在本地登录”  ，再右键单击“属性”  。  
  
4.  单击 **“添加用户或组”** 。  
  
5.  单击 **“位置”** ，指定要搜索的域或其他位置，然后单击 **“确定”** 。  
  
6.  输入要允许其进行交互式登录的 Windows 帐户，然后单击 **“确定”** 。  
  
7.  在 **“允许在本地登录属性”** 对话框中，单击 **“确定”** 。  
  
8.  确保您选择的帐户也没有拒绝权限：  
  
    1.  右键单击“拒绝本地登录”  ，再右键单击“属性”  。  
  
    2.  如果列出了该帐户，则将其选中，然后单击 **“删除”** 。  
  
#### <a name="using-impersonation-with-stored-credentials"></a>对已存储凭据使用模拟功能  
 您还可以使用凭据来模拟其他用户的身份。 对于 SQL Server 数据库，使用模拟选项可以设置 [SETUSER](../../t-sql/statements/setuser-transact-sql.md) 函数。  
  
> [!IMPORTANT]  
>  对于支持订阅的报表，或按计划生成报表历史记录或刷新报表执行快照的报表，请勿使用模拟功能。  
  
### <a name="no-credentials"></a>无凭据  
 您可以将数据源连接配置为不使用凭据。 Microsoft 建议您始终使用凭据访问数据源；并不建议不使用任何凭据。 不过，在以下情况下，可以选择不使用凭据运行报表：  
  
-   远程数据源不要求使用凭据。  
  
-   凭据是在连接字符串中传递的（建议只用于安全连接）。  
  
-   报表是一个使用了父报表的凭据的子报表。  
  
 上述情况下，报表服务器使用一个您必须事先定义的无人参与的执行帐户连接到远程数据源。 由于报表服务器不能使用它的服务凭据连接到远程服务器，因此必须指定一个可由报表服务器用于建立连接的帐户。 有关创建此帐户的详细信息，请参阅[配置无人参与的执行帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
## <a name="user-name-and-password-login"></a>使用用户名和密码登录  
 选择 **“使用此用户名和密码”** 时，必须提供用户名和密码才能访问数据源。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，凭据针对的可能是数据库登录。 凭据将传递到数据源用于身份验证。  
  
##  <a name="DataSourceConfigurationConnections"></a> 数据源配置和网络连接  
 下表显示了如何针对特定的凭据类型和数据处理扩展插件组合建立连接。 如果要使用自定义数据处理扩展插件，请参阅 [指定用于自定义数据处理扩展插件的连接](../../reporting-services/report-data/specify-connections-for-custom-data-processing-extensions.md)。  
  
|**类型**|**网络连接上下文**|**数据源类型**<br /><br /> **（SQL Server、Oracle、ODBC、OLE DB、Analysis Services、XML、SAP NetWeaver BI、Hyperion Essbase）**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|集成安全性|模拟当前用户|对于所有数据源类型，均使用当前的用户帐户进行连接。|  
|Windows 凭据|模拟指定的用户|对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC 和 OLE DB：使用模拟用户帐户进行连接。|  
|数据库凭据|模拟无人参与的执行帐户或服务帐户。<br /><br /> （Reporting Services 会在使用服务标识发送连接请求时删除管理员权限）。|对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC 和 OLE DB：<br /><br /> 将用户名和密码追加到连接字符串中。<br /><br /> 对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]：<br /><br /> 如果使用的是 TCP/IP 协议，则连接会成功；否则，连接将失败。<br /><br /> 对于 XML：<br /><br /> 如果使用数据库凭据，则报表服务器上的连接将失败。|  
|None|模拟无人参与的执行帐户。|对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC 和 OLE DB：<br /><br /> 使用连接字符串中定义的凭据。 如果未定义无人参与的执行帐户，则报表服务器上的连接将失败。<br /><br /> 对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]：<br /><br /> 如果未指定任何凭据，则即使定义了无人参与的执行帐户，连接也总会失败。<br /><br /> 对于 XML：<br /><br /> 如果定义了无人参与的执行帐户，则以匿名用户的身份连接；否则，连接将失败。|  
  
## <a name="setting-credentials-programmatically"></a>通过编程方式设置凭据  
 您可以通过编写代码来设置凭据，以控制对报表和报表服务器的访问。 有关详细信息，请参阅 [Data Sources and Connection Methods](../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 支持的数据源 (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   
 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [管理报表数据源](../../reporting-services/report-data/manage-report-data-sources.md)   
 [配置报表的数据源属性](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
