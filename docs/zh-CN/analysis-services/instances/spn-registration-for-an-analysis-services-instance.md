---
title: 针对 Analysis Services 实例的 SPN 注册 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f210d29986e325c0b444ab30430afbe64d1ff38b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spn-registration-for-an-analysis-services-instance"></a>针对 Analysis Services 实例的 SPN 注册
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在使用 Kerberos 对客户端和服务标识进行相互身份验证时，服务主体名称 (SPN) 唯一标识 Active Directory 域中的某一服务实例。 SPN 与服务实例运行所基于的登录帐户相关联。  
  
 对于通过 Kerberos 身份验证连接到 Analysis Services 的客户端应用程序，Analysis Services 客户端库使用来自连接字符串的主机名以及在 Analysis Services 的任何给定发行版中固定的其他已知变量（例如服务类）构建一个 SPN。  
  
 为进行相互身份验证，客户端所构建的 SPN 必须匹配 Active Directory 域控制器 (DC) 上的相应 SPN 对象。 这意味着，您对于单个 Analysis Services 实例可能需要注册多个 SPN，以便涵盖用户在连接字符串上指定主机名所可能采用的所有方法。 例如，您可能需要两个 SPN 以便处理某个服务器的完全限定域名 (FQDN) 以及短计算机名称。 正确注册 Analysis Services SPN 是成功连接所必需的。 如果该 SPN 不存在、格式错误或重复，则连接将失败。  
  
 SPN 注册是由 Analysis Services 管理员执行的手动任务。 与 SQL Server 数据库引擎不同，Analysis Services 永远不会在服务启动时自动注册其 SPN。 当使用默认虚拟帐户、域用户帐户或内置帐户（包括服务 SID）运行 Analysis Services 时，必须进行手动注册。  
  
 当使用由域管理员创建的预定义托管服务帐户运行服务时，不需要进行 SPN 注册。 请注意，根据您的域的功能级别，注册 SPN 可能要求域管理员权限。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 是一款诊断工具，可帮助解决与 Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相关的连接问题。 有关详细信息，请参阅 [Microsoft Kerberos Configuration Manager for SQL Server](http://www.microsoft.com/download/details.aspx?id=39046)。  
  
 本主题包含以下各节：  
  
 [在需要 SPN 注册时](#bkmk_scnearios)  
  
 [针对 Analysis Services 的 SPN 格式](#bkmk_SPNSyntax)  
  
 [虚拟帐户的 SPN 注册](#bkmk_virtual)  
  
 [域帐户的 SPN 注册](#bkmk_domain)  
  
 [内置帐户的 SPN 注册](#bkmk_builtin)  
  
 [针对命名实例的 SPN 注册](#bkmk_spnNamed)  
  
 [针对 SSAS 群集的 SPN 注册](#bkmk_spnCluster)  
  
 [针对为 HTTP 访问配置的 SSAS 实例的 SPN 注册](#bkmk_spnHTTP)  
  
 [针对在固定端口上侦听的 SSAS 实例的 SPN 注册](#bkmk_spnFixedPorts)  
  
##  <a name="bkmk_scnearios"></a> 在需要 SPN 注册时  
 在连接字符串上指定“SSPI=Kerberos”的任何客户端连接都将引入针对 Analysis Services 实例的 SPN 注册要求。  
  
 在下列情况下需要 SPN 注册。 有关详细信息，请参阅 [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)。  
  
-   将用户标识从客户端应用程序或中间层服务流到 Analysis Services 需要标识委托。 在特定对象上定义每个用户的权限或筛选时，通常会使用标识委托。  
  
     涉及标识委托的常见情形如下：在 Analysis Services 中检索数据时，配置中间层服务（例如 Excel Services 或 Reporting Services）进行约束委托，以模拟用户标识。 为支持此行为，在配置 Excel Services 或 Reporting Services 进行约束委托时，您必须提供 Analysis Services SPN 作为目标服务。  
  
-   Analysis Services 在使用 DirectQuery 模式从 SQL Server 关系数据库为表格数据库检索数据时委托用户标识。 这是 Analysis Services 会将用户标识委托给其他服务的唯一情形。  
  
##  <a name="bkmk_SPNSyntax"></a> 针对 Analysis Services 的 SPN 格式  
 使用 **“setspn”** 注册 SPN。 在较新的操作系统上， **“setspn”** 作为系统实用工具安装。 有关详细信息，请参阅 [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx)。  
  
 下表介绍 Analysis Services SPN 的每个部分。  
  
|元素|Description|  
|-------------|-----------------|  
|服务类|MSOLAPSvc.3 将服务标识为 Analysis Services 实例。 .3 表示在 Analysis Services 传输中使用的 XMLA-over-TCP/IP 协议的版本。 它与产品发行版无关。 因此，在修订协议本身之前，MSOLAPSvc.3 是针对 SQL Server 2005、2008、2008 R2、2012 和 Analysis Services 的任何将来发行版的正确的服务类。|  
|主机名称|标识正在运行服务的计算机。 该名称可以是完全限定域名称或 NetBIOS 名称。 应当为二者都注册 SPN。<br /><br /> 为服务器 NetBIOS 名称注册 SPN 时，务必使用 `SetupSPN –S` 检查是否存在重复的注册。 我们不保证 NetBIOS 名称在林中是唯一的，而拥有重复 SPN 注册可能会导致连接失败。<br /><br /> 对于 Analysis Services 负载平衡群集，主机名应该是分配给群集的虚拟名称。<br /><br /> 切勿使用 IP 地址创建 SPN。 Kerberos 使用域的 DNS 解析功能。 指定 IP 地址会绕过该功能。|  
|端口号|尽管端口号是 SPN 语法的一部分，但在注册 Analysis Services SPN 时切勿指定端口号。 冒号 ( : ) 字符通常用于在标准 SPN 语法中提供端口号，由 Analysis Services 用来指定实例名称。 对于 Analysis Services 实例，假定端口是默认端口 (TCP 2383) 或者 SQL Server Browser 服务分配的端口 (TCP 2382)。|  
|实例名称|Analysis Services 是可以在同一台计算机上多次安装的可复制的服务。 通过其实例名称标识每个实例。<br /><br /> 该实例名称以冒号 ( : ) 字符作为前缀。 例如，假定一个名为 SRV01 的主机以及一个 SSAS-Tabular 命名实例，则 SPN 应该是 SRV01:SSAS-Tabular。<br /><br /> 请注意，用于指定命名 Analysis Services 实例的语法不同于其他 SQL Server 实例使用的语法。 其他服务使用反斜杠 ( \ ) 在 SPN 中追加实例名称。|  
|服务帐户|这是 **“MSSQLServerOLAPService”** Windows 服务的启动帐户。 它可以是 Windows 域用户帐户、虚拟帐户、托管服务帐户 (MSA) 或内置帐户，例如服务 SID、NetworkService 或 LocalSystem。 Windows 域用户帐户可进行格式设置为域 \ 用户或user@domain。|  
  
##  <a name="bkmk_virtual"></a> 虚拟帐户的 SPN 注册  
 对于 SQL Server 服务，虚拟帐户是默认的帐户类型。 虚拟帐户是**NT Service\MSOLAPService**对于默认实例和**NT Service\MSOLAP$**\<实例名称 > 对于命名实例。  
  
 如名称所示，这些帐户不存在于 Active Directory 中。 虚拟帐户只存在于本地计算机上。 连接外部服务、应用程序或设备时，使用本地计算机帐户进行连接。 因此，在虚拟帐户上运行 Analysis Services 的 SPN 注册实际上是计算机帐户的 SPN 注册。  
  
 **以 NT Service\MSOLAPService 身份运行的默认实例的示例语法**  
  
 此示例为在默认虚拟帐户下运行的 Analysis Services 默认实例显示 **“setspn”** 语法。 在此示例中，计算机主机名为 **AW-SRV01**。 如前所述，SPN 注册必须指定“计算机帐户”  而不是虚拟帐户 **“NT Service\MSOLAPService”**。  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
> [!NOTE]  
>  请记得创建两个 SPN 注册，一个用于 NetBIOS 主机名，另一个用于完全限定的主机域名。 在连接 Analysis Services 时，不同的客户端应用程序使用不同的主机名约定。 有两个 SPN 注册可确保这两个版本的主机名都考虑在内。  
  
 **对于命名实例作为 NT Service\MSOLAP$ 运行的示例语法\<实例名称 >**  
  
 此示例为在默认虚拟帐户下运行的 Analysis Services 命名实例显示 **“setspn”** 语法。 在此示例中，计算机主机名为 **AW-SRV02**，实例名为 **AW-FINANCE**。 同样，它是 SPN，为指定的计算机帐户，而不是虚拟帐户**NT Service\MSOLAP$**\<实例名称 >。  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV02.AdventureWorks.com:AW-FINANCE AW-SRV02  
```  
  
##  <a name="bkmk_domain"></a> 域帐户的 SPN 注册  
 使用域帐户运行 Analysis Services 实例是一种常见做法。  
  
 对于在网络或硬件负载平衡的群集中运行的 Analysis Services 实例而言，需要使用域帐户，且群集中每个实例都在相同的域帐户下运行。  
  
 **以域用户身份运行的默认实例的示例语法**  
  
 此示例为在 AdventureWorks 域的域用户帐户 **SSAS-Service** 之下运行的 Analysis Services 默认实例显示 **setspn**语法。  
  
```  
Setspn –s msolapsvc.3\AW-SRV01.Adventureworks.com AdventureWorks\SSAS-Service  
```  
  
> [!TIP]  
>  通过运行 `Setspn -L <domain account>` 或 `Setspn -L <machinename>`（取决于注册 SPN 的方式），验证是否已为 Analysis Services 服务器创建了 SPN。 你应看到 MSOLAPSVC.3/\<主机名 > 列表中。  
  
##  <a name="bkmk_builtin"></a> 内置帐户的 SPN 注册  
 尽管不建议采用这种做法，但是旧版的 Analysis Services 安装有时会配置为在内置帐户（如 Network Service、Local Service 或 Local System）下运行。  
  
 **以内置帐户身份运行的默认实例的示例语法**  
  
 在内置帐户或各服务的SID 下运行的服务的 SPN 注册相当于虚拟帐户使用的 SPN 语法。 不使用帐户名，而是使用机器帐户：  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnNamed"></a> 针对命名实例的 SPN 注册  
 Analysis Services 的命名实例会使用 SQL Server Browser 服务检测到的动态端口分配。 使用命名实例时，为 SQL Server Browser Service 和 Analysis Services 命名实例注册 SPN。 有关详细信息，请参阅 [与 SQL Server Analysis Services 或 SQL Server 的命名实例建立连接时，需要提供 SQL Server Browser 服务的 SPN](http://support.microsoft.com/kb/950599)。  
  
 **以 LocalService 身份运行的 SQL Browser Service 的 SPN 示例语法**  
  
 服务类为 **“MSOLAPDisco.3”**。 默认情况下，此服务会以 NT AUTHORITY\LocalService 身份运行，这意味着已为计算机帐户设置了 SPN 注册。 在此示例中，计算机帐户为 **AW-SRV01**，与计算机名相对应。  
  
```  
Setspn -S MSOLAPDisco.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnCluster"></a> 针对 SSAS 群集的 SPN 注册  
 对于 Analysis Services 故障转移群集，主机名应该是分配给群集的虚拟名称。 此为 SQL Server 网络名，是当你在现有 WSFC 基础上安装 Analysis Services 后，SQL Server 安装期间指定的。 可在 Active Directory 中找到此名称。 还可在 **“故障转移群集管理器”** | **“角色”** | **“资源”** 选项卡中找到它。“资源”选项卡上的服务器名应在 SPN 命令中作为“虚拟名称”使用。  
  
 **Analysis Services 群集的 SPN 语法**  
  
```  
Setspn –s msolapsvc.3/<virtualname.FQDN > <domain user account>  
```  
  
 请记住，Analysis Services 群集中的节点需要使用默认端口 (TCP 2383) 并且在相同的域用户帐户下运行，以便每个节点都具有相同的 SID。 有关详细信息，请参阅 [如何安装群集 SQL Server Analysis Services](http://msdn.microsoft.com/library/dn736073.aspx) 。  
  
##  <a name="bkmk_spnHTTP"></a> 针对为 HTTP 访问配置的 SSAS 实例的 SPN 注册  
 根据解决方案要求，您可能已经针对 HTTP 访问配置了 Analysis Services。 如果您的解决方案将 IIS 作为一个中间层组件包括，并且 Kerberos 身份验证是解决方案要求，则您可能需要手动为 IIS 注册 SPN。 有关详细信息，请参阅 [如何配置 SQL Server 2008 Analysis Services 和 SQL Server 2005 Analysis Services 以便使用 Kerberos 身份验证](http://support.microsoft.com/kb/917409)中的“在运行 IIS 的计算机上配置设置”。  
  
 就针对 Analysis Services 实例的 SPN 注册而言，在为 TCP 或 HTTP 配置的实例之间没有差别。 使用 MSMDPUMP ISAPI 扩展插件从 IIS 到 Analysis Services 的连接始终是 TCP。  
  
 这意味着，您可以使用前面几节中针对默认实例或命名实例的说明来注册 SPN。 在指定主机名时，请确保使用您在为 HTTP 访问配置服务时在 msmdpump.ini 文件中指定的主机名。  
  
 有关 HTTP 访问的详细信息，请参阅[在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
##  <a name="bkmk_spnFixedPorts"></a> 针对在固定端口上侦听的 SSAS 实例的 SPN 注册  
 您不能在 Analysis Services SPN 注册上指定端口号。 如果您将 Analysis Services 作为默认实例安装并且将其配置为侦听某一固定端口，则现在必须将其配置为侦听默认端口 (TCP 2383)。 对于命名实例，您需要使用 SQL Server Browser 服务和动态端口分配。  
  
 一个 Analysis Services 实例只能侦听单个端口。 不支持使用多个端口。 有关端口配置的详细信息，请参阅 [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft BI 身份验证和身份委托](http://go.microsoft.com/fwlink/?LinkID=286576)   
 [使用 Kerberos 进行相互身份验证](http://go.microsoft.com/fwlink/?LinkId=299283)   
 [如何配置 SQL Server 2008 Analysis Services 和 SQL Server 2005 Analysis Services 以便使用 Kerberos 身份验证](http://support.microsoft.com/kb/917409)   
 [服务主体名称 (SPN) SetSPN 语法 (Setspn.exe)](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [我使用哪个 SPN，它如何起作用？](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx)   
 [服务帐户分步指南](http://technet.microsoft.com/library/dd548356\(WS.10\).aspx)   
 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [在配置托管在 Internet Information Services 上的 Web 应用程序时，如何使用 SPN](http://support.microsoft.com/kb/929650)   
 [服务帐户中的新增功能有哪些](http://technet.microsoft.com/library/dd367859\(WS.10\).aspx)   
 [配置用于 SharePoint 2010 产品的 Kerberos 身份验证（白皮书）](http://technet.microsoft.com/library/ff829837.aspx)  
  
  
