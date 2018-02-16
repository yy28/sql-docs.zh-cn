---
title: "安装向导帮助 | Microsoft Docs"
ms.custom: 
ms.date: 2017-04-21
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
caps.latest.revision: 
ms.author: mikeray
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 16c42d4f6864e94c475ba917c75c8219d96245ce
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="installation-wizard-help"></a>安装向导帮助
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导中的一些配置页。 

## <a name="instance-configuration"></a>实例配置
使用 **安装向导的** “实例配置” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页面可指定是创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的默认实例还是其命名实例。 如果尚未安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，则除非您指定命名实例，否则将创建默认实例。  
  
每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例都由一组具有排列规则及其他选项特定设置的非重复的服务组成。 目录结构、注册表结构和服务名称都反映在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中创建的实例名称和特定实例 ID。  
  
 实例是默认实例或命名实例。 默认实例名为 MSSQLSERVER。 不需要客户端指定实例名称便可进行连接。 命名实例在安装过程中由用户决定。 您可以将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作为命名实例安装，无需先安装默认实例。 不论版本如何，一次均只能安装一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]默认实例。  
  
> [!NOTE]  
> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep，您可以在 **“实例配置”** 页上完成已准备实例时指定实例名称。 如果在计算机上没有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的现有默认实例，您可以选择将正在完成的已准备实例配置为默认实例。  
  
### <a name="multiple-instances"></a>多实例  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持在单个服务器或处理器上存在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，但只能有一个实例为默认实例。 所有其他实例必须为命名实例。 一台计算机可同时运行多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，每个实例独立于其他实例运行。  
  
 有关详细信息，请参阅 [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md)。  
  
### <a name="options"></a>“常规”  
 仅限故障转移群集实例 - 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集网络名称。 此名称可用来在网络上标识故障转移群集实例。  
  
 默认实例或命名实例 - 当您决定是安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的默认实例还是命名实例时，请考虑以下信息：  
  
-   如果计划在数据库服务器上安装单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，则该实例应为默认实例。  
  
-   如果您打算在同一台计算机上安装多个实例，请使用命名实例。 一台服务器只能承载一个默认实例。  
  
-   任何安装 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的应用程序都应将其作为命名实例安装。 当同一台计算机中安装多个应用程序时，这样可以最大程度地减少冲突。  
  
 **默认实例**  
 选择该选项可安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例。 一台计算机只能承载一个默认实例；所有其他实例必须是命名实例。 但是，如果您已经安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例，则可以向同一台计算机添加 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的默认实例。  
  
 **命名实例**  
 选择该选项可创建新的命名实例。 当对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行命名时，请注意以下几点：  
  
-   实例名不区分大小写。  
  
-   实例名不能以下划线 (_) 开始或结束。  
  
-   实例名称不能包含词语“Default”或其他保留关键字。 如果在实例名中使用了保留关键字，将发生安装错误。 有关详细信息，请参阅[保留关键字 (Transact-SQL) ](../../t-sql/language-elements/reserved-keywords-transact-sql.md)。  
  
-   如果为实例名称指定 MSSQLServer，将创建默认实例。  
  
-   [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 的安装始终安装为“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]”的命名实例。 您不能为此功能角色指定不同的实例名称。  
  
-   实例名限制为 16 个字符。  
  
-   实例名中的第一个字符必须是字母。 可接受的字母为 Unicode 标准 2.0 定义的那些字母。 这些字母包括拉丁字符 a-z、A-Z 和其他语言中的字母字符。  
  
-   后续字符可以是 Unicode 标准 2.0 定义的字母、源于基本拉丁语或其他国家/地区书写符号的十进制数字、美元符号 ($) 或者下划线 (_)。  
  
-   实例名称中不允许含有空格或其他特殊字符， 也不允许存在反斜杠 (\\)、逗号 (,)、冒号 (:)、分号 (;)、单引号 (')、& 号 (&)、连字号 (-) 和 at 符 (@)。  
  
     只有在当前 Windows 代码页中有效的字符才能用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称中。 如果使用了不支持的 Unicode 字符，将会发生安装错误。  
  
 **检测到的实例和功能**  
 查看正在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的计算机中安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和组件的列表。  
  
 **实例 ID** - 默认情况下，实例名称用作实例 ID。 这用于标识 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的安装目录和注册表项。 默认实例和命名实例的默认方式都是如此。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认的实例 ID，请在 **实例 ID** 字段中指定它。  
  
> [!IMPORTANT]  
>  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep，在此页上显示的实例 ID 是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 过程的准备映像步骤中指定的实例 ID。 在完成映像步骤中，您将无法指定不同的实例 ID。  
  
> [!NOTE]  
>  不支持以下划线 (_) 开头或者包含数字符号 (#) 或美元符号 ($) 的实例 ID。  
  
 有关目录、文件位置和实例 ID 命名的详细信息，请参阅 [默认和已命名的 SQL Server 实例的文件位置](file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的给定实例的所有组件作为一个单元进行管理。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升级都将应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的每个组件。  
  
 共用同一实例名称的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件都必须满足以下条件：  
  
-   版本相同  
  
-   版本类别相同  
  
-   语言设置相同  
  
-   聚集状态相同  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不能识别群集。  
  
-   操作系统相同  
  
## <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services 配置 – 帐户设置
  使用此页可以设置服务器节点，并向要求对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进行不受限访问的用户或服务授予管理权限。 安装程序不会自动将本地 Windows 组 BUILTIN\Administrators 添加到要安装的实例的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器管理员角色。 如果您想要将本地管理员组添加到服务器管理员角色，则必须显式指定该组。  
  
 如果您正在安装 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，确保将管理权限授予负责在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 场中部署 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 服务器的 SharePoint 场管理员或服务管理员。  
  
### <a name="options"></a>“常规”  
 **服务器模式** - 服务器模式指定可部署到服务器的 Analysis Services 数据库的类型。 服务器模式在安装过程中确定，之后不能修改。 各模式是互斥的，也就是说，您需要两个 Analysis Services 实例，它们配置为不同的模式，以便同时支持典型 OLAP 和表格模型解决方案。  
  
 **指定管理员** - 必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例指定至少一个服务器管理员。 您指定的用户或组将成为所安装的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器管理员角色的成员。 这些都必须是与安装该软件的计算机处于同一域中的 Windows 域用户帐户。  
  
> [!NOTE]  
>  用户帐户控制 (UAC) 是一个 Windows 安全功能，它要求在运行管理操作或应用程序之前，先由管理员专门审批。 由于 UAC 在默认情况下处于打开状态，因此系统将提示您允许需要提升权限的特定操作。 您可以配置 UAC 来更改默认行为，或针对特定程序自定义 UAC。 有关 UAC 和 UAC 配置的详细信息，请参阅 [User Account Control Step by Step Guide](http://go.microsoft.com/fwlink/?linkid=196350)（用户帐户控制分步指南）和 [User Account Control (Wikipedia)](http://go.microsoft.com/fwlink/?linkid=196351)（用户帐户控制 (Wikipedia)）。  
  
### <a name="see-also"></a>另请参阅  
 [配置服务帐户 (Analysis Services)](../../analysis-services/instances/configure-service-accounts-analysis-services.md) [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

 ## <a name="analysis-services-configuration---data-directories"></a>Analysis Services 配置 - 数据目录
  下表中的默认目录是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中可由用户配置的目录。 访问这些文件的权限授予了本地管理员和安装过程中创建并配置的 SQLServerMSASUser$\< 实例 > 安全组成员。  
  
### <a name="uielement-list"></a>UIElement 列表  
  
|Description|默认目录|建议|  
|-----------------|-----------------------|---------------------|  
|数据根目录|C:\Program Files\Microsoft SQL Server\MSASnn.\<InstanceID>\OLAP\Data\ |确保通过限制权限对 \Program files\Microsoft SQL Server\ 文件夹进行保护。 在许多配置中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 性能取决于数据目录所在的存储区的性能。 请将此目录放置在附加到系统上的最高性能存储区中。 对于故障转移群集安装，应确保数据目录位于共享磁盘上。|  
|日志文件目录|C:\Program Files\Microsoft SQL Server\MSASnn.\<InstanceID>\OLAP\Log\ |这是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 日志文件的目录，该目录包含 FlightRecorder 日志。 如果要延长网络流量记录器持续时间，请确保该日志目录有足够的空间。|  
|Temp 目录|C:\Program Files\Microsoft SQL Server\MSASnn.\<InstanceID>\OLAP\Temp\ |将 Temp 目录放置在高性能存储子系统中。|  
|备份目录|C:\Program Files\Microsoft SQL Server\MSASnn.\<InstanceID>\OLAP\Backup\ |这是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 默认备份文件的目录。 对于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装，这也是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务缓存 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据文件的位置。<br /><br /> 确保设置合适的权限以防止数据丢失，并确保 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务的用户组具有写入备份目录的足够权限。 不支持对备份目录使用映射的驱动器。|  
  
### <a name="notes"></a>说明  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署到 SharePoint 场中的实例将应用程序文件、数据文件和属性存储于内容数据库和服务应用程序数据库中。  
  
-   向现有安装添加功能时，不能更改以前安装的功能的位置，也不能为新功能指定该位置。  

-   可能需要安装扫描软件（如防病毒应用程序和反间谍应用程序）以排除 SQL Server 文件夹和文件类型。 有关详细信息，请查看支持文章：[运行 SQL Server 的计算机上的防病毒软件](https://support.microsoft.com/kb/309422)。
  
-   如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件也应安装到单独的目录。  
  
-   在下列情况下，不能安装程序文件和数据文件：  
  
    -   在可移动磁盘驱动器上  
  
    -   在使用压缩的文件系统上  
  
    -   在系统文件所在的目录上  
  
### <a name="see-also"></a>另请参阅  
 有关目录、文件位置和实例 ID 命名的详细信息，请参阅 [默认和已命名的 SQL Server 实例的文件位置](file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
## <a name="database-engine-configuration---data-directories"></a>数据库引擎配置 - 数据目录
  使用此页面可指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 程序和数据文件的安装位置。 根据安装类型，支持的存储可能包括本地磁盘、共享存储或 SMB 文件服务器。  
  
 若要将 SMB 文件共享指定为目录，您必须手动键入支持的 UNC 路径。 不支持浏览到 SMB 文件共享。 下面是 SMB 文件共享支持的 UNC 路径格式： \\\Servername\ShareName\\....  
  
### <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的独立实例  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的独立实例支持的存储类型和默认目录，用户可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中配置这些内容。  
  
### <a name="uielement-list"></a>UIElement 列表  
  
|Description|支持的存储类型|默认目录|建议|  
|-----------------|----------------------------|-----------------------|---------------------|  
|数据根目录|本地磁盘、SMB 文件服务器、共享存储* |C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录配置 ACL 并在配置过程中中断继承。|  
|用户数据库目录|本地磁盘、SMB 文件服务器、共享存储*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Data |用户数据目录的最佳实践取决于工作量和性能要求。|  
|用户数据库日志目录|本地磁盘、SMB 文件服务器、共享存储*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Data|确保日志目录有足够的空间。|  
|备份目录|本地磁盘、SMB 文件服务器、共享存储*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Backup|设置合适的权限以防止数据丢失，并确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的用户帐户具有写入备份目录的足够权限。 不支持对备份目录使用映射的驱动器。|  
  
 *尽管支持共享磁盘，但不建议对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的独立实例采用这种做法。  
  
### <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的故障转移群集实例支持的存储类型和默认目录，用户可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中配置这些内容。  
  
|Description|支持的存储类型|默认目录|建议|  
|-----------------|----------------------------|-----------------------|---------------------|  
|数据根目录|共享存储、SMB 文件服务器|\<驱动器:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> 提示：如果在“群集磁盘选择”  页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录配置 ACL 并在配置过程中中断继承。|  
|用户数据库目录|共享存储、SMB 文件服务器|\<Drive:>Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Data<br /><br /> 提示：如果在“群集磁盘选择”  页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|用户数据目录的最佳实践取决于工作量和性能要求。|  
|用户数据库日志目录|共享存储、SMB 文件服务器|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Data<br /><br /> 提示：如果在“群集磁盘选择”  页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|确保日志目录有足够的空间。|  
|备份目录|本地磁盘、共享存储、SMB 文件服务器|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Backup<br /><br /> 提示：如果在“群集磁盘选择”  页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|设置合适的权限以防止数据丢失，并确保 SQL Server 服务的用户帐户具有写入备份目录的足够权限。 不支持对备份目录使用映射的驱动器。|  
  
### <a name="security-considerations"></a>需要考虑的安全性因素  
 安装程序将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录配置 ACL 并在配置过程中中断继承。  
  
 以下建议适用于 SMB 文件服务器：  
  
-   使用 SMB 文件服务器时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户必须是域帐户。  
  
-   用于安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帐户应对用作数据目录的 SMB 文件共享文件夹具有 FULL CONTROL NTFS 权限。  
  
-   用于安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帐户应具有对 SMB 文件服务器的 SeSecurityPrivilege 特权。 若要授予此特权，请使用文件服务器上的“本地安全策略”控制台将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装帐户添加到 **“管理审核和安全日志”** 策略中。 在 **“本地安全策略”** 控制台中 **“本地策略”** 下的 **“用户权限分配”** 部分可以找到此设置。  
  
### <a name="notes"></a>说明  
  
-   向现有安装中添加功能时，不能更改先前安装的功能的位置，也不能为新功能指定该位置。  
  
-   如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件也应安装到单独的目录。  
  
-   在下列情况下，不能安装程序文件和数据文件：  
  
    -   在可移动磁盘驱动器上  
  
    -   在使用压缩的文件系统上  
  
    -   在系统文件所在的目录上  
  
    -   在故障转移群集实例的映射网络驱动器上  
  
### <a name="see-also"></a>另请参阅  
### <a name="analysis-services-configuration---data-directories"></a>Analysis Services 配置 - 数据目录
  下表中的默认目录是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中可由用户配置的目录。 访问这些文件的权限授予了本地管理员和安装过程中创建并配置的 SQLServerMSASUser$\< 实例 > 安全组成员。  
  
#### <a name="uielement-list"></a>UIElement 列表  
  
|Description|默认目录|建议|  
|-----------------|-----------------------|---------------------|  
|数据根目录 |C:\Program Files\Microsoft SQL Server\MSASnn.\<InstanceID>\OLAP\Data |确保通过限制权限对 \Program files\Microsoft SQL Server\ 文件夹进行保护。 在许多配置中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 性能取决于数据目录所在的存储区的性能。 请将此目录放置在附加到系统上的最高性能存储区中。 对于故障转移群集安装，应确保数据目录位于共享磁盘上。|  
|日志文件目录|C:\Program Files\Microsoft SQL Server\MSASnn.\<InstanceID>\OLAP\Log |这是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 日志文件的目录，该目录包含 FlightRecorder 日志。 如果要延长网络流量记录器持续时间，请确保该日志目录有足够的空间。|  
|Temp 目录|C:\Program Files\Microsoft SQL Server\MSASnn.\<InstanceID>\OLAP\Temp |将 Temp 目录放置在高性能存储子系统中。|  
|备份目录|C:\Program Files\Microsoft SQL Server\MSASnn.\<InstanceID>\OLAP\Backup |这是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 默认备份文件的目录。 对于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装，这也是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务缓存 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据文件的位置。<br /><br /> 确保设置合适的权限以防止数据丢失，并确保 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务的用户组具有写入备份目录的足够权限。 不支持对备份目录使用映射的驱动器。|  
  
#### <a name="notes"></a>说明  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署到 SharePoint 场中的实例将应用程序文件、数据文件和属性存储于内容数据库和服务应用程序数据库中。  
  
-   向现有安装添加功能时，不能更改以前安装的功能的位置，也不能为新功能指定该位置。  

-   可能需要安装扫描软件（如防病毒应用程序和反间谍应用程序）以排除 SQL Server 文件夹和文件类型。 有关详细信息，请查看支持文章：[运行 SQL Server 的计算机上的防病毒软件](https://support.microsoft.com/kb/309422)。
  
-   如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件也应安装到单独的目录。  
  
-   在下列情况下，不能安装程序文件和数据文件：  
  
    -   在可移动磁盘驱动器上  
  
    -   在使用压缩的文件系统上  
  
    -   在系统文件所在的目录上  
  
#### <a name="see-also"></a>另请参阅  
 有关目录、文件位置和实例 ID 命名的详细信息，请参阅 [默认和已命名的 SQL Server 实例的文件位置](file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
    
 [文件服务器上的共享权限和 NTFS 权限](http://go.microsoft.com/fwlink/?LinkID=206571) 

## <a name="database-engine-configuration---filestream"></a>数据库引擎配置 - 文件流
  使用此页可针对此 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装启用 FILESTREAM。 FILESTREAM 通过将 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] varbinary(max) **二进制大型对象 (BLOB) 数据作为文件存储在 NTFS 文件系统中，将** 与该文件系统集成在一起。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可插入、更新、查询、搜索和备份 FILESTREAM 数据。 通过 Win32 文件系统接口可以流式方式访问数据。  
  
### <a name="uielement-list"></a>UIElement 列表  
 **针对 Transact-SQL 访问启用 FILESTREAM**  
 选中此项可针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问启用 FILESTREAM。 必须选中此控制选项，才能使用其他控制选项。  
  
 **针对文件 I/O 流访问启用 FILESTREAM**  
 选中此项可针对 FILESTREAM 启用 Win32 流访问。  
  
 **Windows 共享名**  
 使用此控制选项可输入将用来存储 FILESTREAM 数据的 Windows 共享的名称。  
  
 **允许远程客户端针对 FILESTREAM 数据启用流访问**  
 选中此控制选项可允许远程客户端访问此服务器上的此 FILESTREAM 数据。  
  
### <a name="see-also"></a>另请参阅  
 [启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

  
## <a name="database-engine-configuration---server-configuration"></a>数据库引擎配置 - 服务器配置
  使用此页可以设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全模式，并添加 Windows 用户或组作为 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的管理员。  
  
### <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>有关运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的注意事项  
 在以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，将 **BUILTIN\Administrators** 组设置为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中的登录名，本地 Administrators 组的成员可以使用其管理员凭据登录。 使用提升的权限并不是最好的做法。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，未将 **BUILTIN\Administrators** 组设置为登录名。 因此，您应为每个管理用户创建一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，并在安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新实例的过程中将该登录名添加到 sysadmin 固定服务器角色中。 对于用来运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的 Windows 帐户，您也应该执行这些操作。 这些作业包括复制代理作业。  
  
### <a name="options"></a>“常规”  
 **安全模式** - 选择“Windows 身份验证”或“混合模式身份验证”用于安装。  
  
 **Windows 主体设置** - 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的早期版本中，Windows Builtin\Administrator 本地组放入了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 服务器角色中，有效授予了 Windows 管理员对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的访问权限。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的 sysadmin 服务器角色中未设置 Builtin\Administrator 组， 而是改为由您在安装过程中为新安装显式设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员。  
  
> [!IMPORTANT]  
>  您在安装过程中必须为新安装显式设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员。 直到您完成此步骤之后，安装程序才允许您继续操作。  
  
 **指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员** - 必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例至少指定一个 Windows 主体。 若要添加用以运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的帐户，请单击 **“当前用户”** 按钮。 若要向系统管理员列表中添加帐户或从中删除帐户，请单击 **“添加”** 或 **“删除”**，然后编辑将拥有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的管理员权限的用户、组或计算机的列表。  
  
 完成列表的编辑后，单击 **“确定”**，然后在配置对话框中验证管理员列表。 完成此列表后，请单击 **“下一步”**。  
  
 如果选择“混合模式身份验证”，则必须为内置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员 (SA) 帐户提供登录凭据。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Windows 身份验证模式**  
 当用户通过 Windows 用户帐户连接时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用操作系统中的 Windows 主体标记验证帐户名和密码。 此为默认身份验证模式，比混合模式更为安全。 Windows 身份验证利用 Kerberos 安全协议，通过强密码的复杂性验证提供密码策略强制，提供帐户锁定支持，并且支持密码过期。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 切勿设置空密码或弱 sa 密码。  
  
 **混合模式（Windows 身份验证或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证）**  
 允许用户使用 Windows 身份验证或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接。 通过 Windows 用户帐户进行连接的用户可以使用经过 Windows 验证的可信连接。  
  
 如果必须选择“混合模式身份验证”并且要求使用 SQL 登录名以适应早期应用程序，则必须为所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户设置强密码。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证只是为了向后兼容。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **输入密码**  
 输入并确认系统管理员 (sa) 登录名。 密码是抵御入侵者的第一道防线，因此设置强密码对于系统安全是绝对必要的。 切勿设置空密码或弱 sa 密码。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密码可包含 1 到 128 个字符，包括字母、符号和数字的任意组合。 如果选择“混合模式身份验证”，则必须输入强 sa 密码才能进入安装向导的下一页。  
  
 **强密码指南**  
 强密码不易被人猜出，也不易用计算机程序攻击。 强密码不能使用禁止的条件或字词，这些条件或字词包括：  
  
-   空条件或 NULL 条件  
  
-   “Password”  
  
-   “Admin”  
  
-   “Administrator”  
  
-   “sa”  
  
-   “sysadmin”  
  
 强密码不能是与安装计算机相关联的下列字词：  
  
-   当前登录到计算机的用户的名称。  
  
-   计算机名称。  
  
 强密码的长度必须多于 8 个字符，并且强密码至少要满足下列四个条件中的三个：  
  
-   它必须包含大写字母。  
  
-   它必须包含小写字母。  
  
-   必须包含数字。  
  
-   必须包含非字母数字字符；例如 #、% 或 ^。  
  
 此页上输入的密码必须符合强密码策略要求。 如果存在任何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的自动化过程，请确保该密码符合强密码策略要求。  
  
### <a name="related-content"></a>相关内容  
 有关选择 Windows 身份验证和有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的信息，请参阅[选择身份验证模式](../../relational-databases/security/choose-an-authentication-mode.md)。  
  
 若要深入了解如何选择帐户来运行 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]，请参阅[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。
  
## <a name="database-engine-configuration---tempdb"></a>数据库引擎配置 - TempDB
  使用此页可指定 tempdb 数据和日志文件位置、大小、增长设置和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 的文件数量。 根据安装类型，支持的存储可能包括本地磁盘、共享存储或 SMB 文件服务器。  
  
 若要将 SMB 文件共享指定为目录，您必须手动键入支持的 UNC 路径。 不支持浏览到 SMB 文件共享。 下面是 SMB 文件共享支持的 UNC 路径格式： \\\Servername\ShareName\\....  
  
### <a name="data-and-log-directories-for--a-stand-alone-instance-of--includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 独立实例的数据和日志目录  
 下表列出了用户可以在安装过程中配置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的独立实例支持的存储类型和默认目录。  
  
|Description|支持的存储类型|默认目录|建议|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**数据目录**|本地磁盘、SMB 文件服务器、共享存储* |C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Data|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录配置 ACL 并在配置过程中中断继承。<br /><br /> **temdb** 目录的最佳实践取决于工作量和性能要求。 指定多个文件夹/驱动器以在多个卷上分布数据文件。|  
|**日志目录**|本地磁盘、SMB 文件服务器、共享存储*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Data|确保日志目录有足够的空间。|  
  
 *尽管支持共享磁盘，但不建议对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的独立实例采用这种做法。  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例的数据和日志目录  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的故障转移群集实例支持的存储类型和默认目录，用户可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中配置这些内容。  
  
|Description|支持的存储类型|默认目录|建议|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**tempdb** 数据目录|本地磁盘、共享存储、SMB 文件服务器|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\Data<br /><br /> 提示：如果在“群集磁盘选择”  页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录配置 ACL 并在配置过程中中断继承。<br /><br /> 确保指定的一个目录或多个目录（如果指定了多个文件）对于所有群集节点有效。 在故障转移期间，如果 **tempdb** 目录在故障转移目标节点上不可用，则 SQL Server 资源将无法联机。|  
|**tempdb** 日志目录|本地磁盘、共享存储、SMB 文件服务器|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQLnn.\<InstanceID>\MSSQL\Data<br /><br /> 提示：如果在“群集磁盘选择”  页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|用户数据目录的最佳实践取决于工作量和性能要求。<br /><br /> 请确保指定的目录对所有群集节点都有效。 在故障转移期间，如果 **tempdb** 目录在故障转移目标节点上不可用，则 SQL Server 资源将无法联机。<br /><br /> 确保日志目录有足够的空间。|  
  
### <a name="uielement-list"></a>UIElement 列表  
 根据工作负荷和要求配置 **tempdb** 的设置。 下列设置适用于 **tempdb** 数据文件：  
  
-   “文件数” 是 **tempdb**的数据文件总数。 默认值为 8 和安装程序检测到了逻辑内核数中的较小值。 一般而言，如果逻辑处理器数小于或等于 8，则使用的数据文件数与逻辑处理器数相同。 如果逻辑处理器数大于 8，则使用 8 个数据文件，如果仍然存在争用，则以 4 的倍数增加数据文件的数量（最多为逻辑处理器的数量），直到争用减少到可接受的级别或对工作负荷/代码进行更改。 
  
-   **初始大小 (MB)** 是每个 **tempdb** 数据文件的初始大小（以 MB 表示）。 默认值为 8 MB（对于 [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)] 为 4 MB）。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 引入的最大初始文件大小为 262,144 MB (256 GB)。 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 的最大初始文件大小为 1024 MB。 所有 **tempdb** 数据文件初始大小相同。 由于每次 SQL Server 启动或故障转移时都会重新创建 **tempdb** ，因此你应指定与你的工作负载正常运行所需大小接近的大小。 若要在启动时进一步优化 **tempdb** 的创建，则启用[数据库实例文件初始化](../../relational-databases/databases/database-instant-file-initialization.md)。  
  
-   **总初始大小 (MB)** 是所有 **tempdb** 数据文件的累积大小。  
  
-   **自动增长 (MB)** 是以 MB 为单位的空间量，是每个 **tempdb** 数据文件空间不足时将自动增长的空间量。 在 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 及更高版本中，所有数据文件都将按此设置中指定的量同时增长。  
  
-   **总自动增长 (MB)** 是每个自动增长事件的累积大小。  
  
-   “数据目录” 显示托管 **tempdb** 数据文件的所有目录。 当存在多个目录时，将以循环方式将数据文件放置在目录中。 例如，如果创建 3 个目录，并指定 8 个数据文件，则将在第一个目录中创建 1、4 和 7 号数据文件。 将在第二个目录中创建 2、5 和 8 号数据文件。 将第三个目录中创建 3 和 6 号数据文件。  
  
-   若要添加目录，请单击“添加…” 。  
  
-   若要删除一个目录，选择该目录，然后单击“删除” 。  
  
 “TempDB 日志文件” 是日志文件名称。 会自动创建该名称。 下列设置仅适用于 **tempdb** 日志文件：  
  
-   **初始大小 (MB)** 是 **tempdb** 日志文件的初始大小。 默认值为 8 MB（对于 [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)] 为 4 MB）。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 引入的最大初始文件大小为 262,144 MB (256 GB)。 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 的最大初始文件大小为 1024 MB。 由于每次 SQL Server 启动或故障转移时都会重新创建 **tempdb** ，因此你应指定与你的工作负载正常运行所需大小接近的大小。 若要在启动时进一步优化 **tempdb** 的创建，则启用[数据库实例文件初始化](../../relational-databases/databases/database-instant-file-initialization.md)。  
  
-   **注意：Tempdb** 使用最小日志记录。 无法备份 **tempdb** 日志。 每次 SQL Server 启动或群集实例故障转移时，会对其进行重新创建。  
  
-   **自动增长 (MB)** 是 **tempdb** 日志以 MB 为单位的增长量。  默认值 64 MB 在初始化期间创建最优数量的虚拟日志文件。  
  
-   **注意：Tempdb** 日志文件不使用即时文件初始化。  
  
-   “日志目录” 是其中创建 **tempdb** 日志文件的日志目录。 只有一个 **tempdb** 日志目录。  
  
### <a name="security-considerations"></a>需要考虑的安全性因素  
 安装程序将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录配置 ACL 并在配置过程中中断继承。  

 以下建议适用于 SMB 文件服务器：  
  
-   使用 SMB 文件服务器时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户必须是域帐户。  
  
-   用于安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帐户应对用作数据目录的 SMB 文件共享文件夹具有 FULL CONTROL NTFS 权限。  
  
-   用于安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帐户应具有对 SMB 文件服务器的 SeSecurityPrivilege 特权。 若要授予此特权，请使用文件服务器上的“本地安全策略”控制台将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装帐户添加到 **“管理审核和安全日志”** 策略中。 在 **“本地安全策略”** 控制台中 **“本地策略”** 下的 **“用户权限分配”** 部分可以找到此设置。  
  
### <a name="notes"></a>说明  
  
-   如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件也应安装到单独的目录。  
  
### <a name="see-also"></a>另请参阅  
 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [文件服务器上的共享权限和 NTFS 权限](http://go.microsoft.com/fwlink/?LinkID=206571)  

## <a name="database-engine-configuration---user-instance"></a>数据库引擎配置 - 用户实例
使用 **“用户实例”** 页可以为不具有管理员权限的用户生成单独的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并可以将用户添加到管理员角色中。  
  
### <a name="option"></a>选项  
 启用用户实例  
 默认值为“启用”。 若要禁用用户实例的功能，请清除此复选框。  
  
 用户实例也称为子实例或客户端实例，是由父实例（作为服务运行的主实例，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）代表用户生成的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]实例。 用户实例作为用户进程在该用户的安全上下文中运行。 用户实例独立于父实例和该计算机上运行的任何其他用户实例。 用户实例功能也称为“作为正常用户运行”(RANU)。  
  
> [!NOTE]  
>  在安装过程中设置为 **sysadmin** 固定服务器角色的成员的登录名都设置为模板数据库中的管理员。 除非被删除，否则它们是用户实例的 **sysadmin** 固定服务器角色的成员。  
  
 将用户添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员角色中  
 默认情况下不启用此选项。 若要将当前安装用户添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员角色中，请选中此复选框。  
  
 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 作为 BUILTIN\Administrators 成员的用户在连接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]时，不会自动添加到 sysadmin 固定服务器角色中。 只有已显式添加到服务器级管理员角色中的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 用户才能管理 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 Built-In\Users 组的任一成员都可连接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 实例，但他们仅拥有执行数据库任务的有限权限。 因此，对于从先前 Windows 版本中的 BUILTIN\Administrators 和 Built-In\Users 继承 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 特权的用户，必须在运行于 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 上的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]实例中为其显式授予管理特权。  
  
 若要在此安装程序完成后对用户角色进行任何更改，请使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 外围应用配置器工具 (SQLSAC.exe)。 若要更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员角色中的用户列表，请单击 **“添加新管理员”** 链接。  
  
 确保“要设置的用户”字段中列出了应更新其权限的用户的 DomainName\UserName。 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “可用权限” **窗格的** 实例列表中选择要更新的角色，然后单击向右箭头。 若要将用户添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的所有可用实例的所有可用角色中，请单击向右双箭头。  
  
 若要在完成选择后实现这些更改， [!INCLUDE[clickOK](../../includes/clickok-md.md)]。 若要在不进行更改的情况下结束使用此工具，请单击 **“取消”**。  
  
  
