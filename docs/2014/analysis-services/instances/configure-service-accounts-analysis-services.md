---
title: 配置服务帐户 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], logon accounts
- logon accounts [Analysis Services]
- accounts [Analysis Services]
- logon accounts [Analysis Services], about logon accounts
ms.assetid: b481bd51-e077-42f6-8598-ce08c1a38716
caps.latest.revision: 52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12c58fcc3e844e820dbea02e93b52854dc25f05f
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348358"
---
# <a name="configure-service-accounts-analysis-services"></a>配置服务帐户 (Analysis Services)
  产品范围的帐户设置在 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)中有文档介绍，该主题提供有关所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务（包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]）的全面服务帐户信息。 请参阅该主题以了解有关有效帐户类型、安装分配的 Windows 特权、文件系统权限、注册表权限等方面的信息。  
  
 该主题提供了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的补充信息，包括表格和群集安装的必要附加权限。 它也介绍了支持服务器操作所需的权限。 例如，你可以配置要在服务账户下执行的处理和查询操作，在这种情况下，你需要授予附加权限使其运作。  
  
-   [分配给 Analysis Services 的 Windows 特权](#bkmk_winpriv)  
  
-   [分配给 Analysis Services 的文件系统权限](#bkmk_FilePermissions)  
  
-   [授予执行特定服务器操作的其他权限](#bkmk_tasks)  
  
 附加配置步骤（此处无文档介绍）是指为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和服务账户注册一个服务主体名称 (SPN)。 此步骤在双跃点方案中将传递身份验证从客户端应用程序启用到后端数据源。 此步骤仅应用于配置给 Kerberos 约束委派的服务。 有关更多说明，请参阅 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md) 。  
  
## <a name="logon-account-recommendations"></a>登录帐户推荐  
 在故障转移群集中，Analysis Services 的所有实例应配置为使用 Windows 域用户帐户。 将相同帐户分配给所有实例。 有关详情，请参见 [如何群集 Analysis Services](http://msdn.microsoft.com/library/dn736073.aspx) 。  
  
 独立实例应使用默认虚拟帐户， **NT Service\MSSQLServerOLAPService**对于默认实例中，或 **NT Service\MSOLAP$ * * * 实例名称*对于命名实例。 此建议适用于所有服务模式（假设 Windows Server 2008 R2 以及更高版本用于操作系统，SQL Server 2012 以及更高版本用于 Analysis Services）中的 Analysis Services 实例。  
  
## <a name="granting-permissions-to-analysis-services"></a>向 Analysis Services 授予权限  
 此部分阐释了 Analysis Services 用于本地、内部操作所需的权限，例如，启动可执行程序、读取配置文件和从数据目录加载数据库。 若要查找关于设置外部数据访问的权限以及与其他服务和应用程序的互操作性的指南，请进一步参阅此主题中的 [授予特定服务器操作的其他权限](#bkmk_tasks) 。  
  
 对于内部操作，Analysis Services 中的权限持有者不是登录帐户，而是安装程序创建的包含 Per-service SID 的本地 Windows 安全组。 向安全组分配权限与以前版本的 Analysis Services 一致。 此外，登录帐户可能随时间而变化，但是 Per-service SID 和本地安全组在服务器安装的生存期内保持不变。 对于 Analysis Services，这使得安全组（而不是登录帐户）成为持有权限的更好选择。 只要手动向服务实例授予权限（无论是文件系统权限还是 Windows 特权），请务必将权限授予为服务器实例创建的本地安全组。  
  
 安全组的名称遵循某种模式。 前缀始终是`SQLServerMSASUser$`后, 跟计算机名称，实例名结尾。 默认实例是`MSSQLSERVER`。 命名实例是在设置过程中提供的名称。  
  
 可以在本地安全设置中查看此安全组：  
  
-   运行 compmgmt.msc |**本地用户和组** | **组** | `SQLServerMSASUser$`\<服务器名称 >`$MSSQLSERVER` （对于默认实例）。  
  
-   双击安全组，查看其成员。  
  
 组的唯一成员是 Per-service SID。 它右侧是登录帐户。 登录帐户名是 cosmetic，要向 Per-service SID 提供上下文。 如果随后更改登录帐户，然后返回此页面，则会注意到，安全组和 Per-service SID 不会更改，但是登录帐户标签会有所不同。  
  
##  <a name="bkmk_winpriv"></a> 分配给 Analysis Services 服务帐户的 Windows 特权  
 Analysis Services 需要操作系统的的权限，来启动服务和请求系统资源。 请求因服务器模式以及实例是否群集而异。 如果你不熟悉 Windows 权限，请参阅 [特权](http://msdn.microsoft.com/library/windows/desktop/aa379306\(v=vs.85\).aspx) 和 [特权常量 (Windows)](/windows/desktop/SecAuthZ/privilege-constants) 了解详细信息。  
  
 Analysis Services 的所有实例都请求 **作为服务登录** (SeServiceLogonRight) 特权。 SQL Server 安装程序在安装期间给你在指定的服务账户上分配特权。 对于在多维和数据挖掘模式中运行的服务器，这是 Analysis Services 服务帐户为独立服务器安装要求的唯一 Windows 特权，也是安装程序为 Analysis Services 配置的唯一特权。 对于群集和表格实例，必须手动添加附加 Windows 特权。  
  
 在表格或多维模式中，故障转移群集实例必须具有 **提高计划优先级** (SeIncreaseBasePriorityPrivilege)。  
  
 表格实例使用以下三个附加特权，它们必须在安装实例后手动授予。  
  
|||  
|-|-|  
|**增加进程工作集** (SeIncreaseWorkingSetPrivilege)|默认情况下，此特权通过 **用户** 安全组对所有用户可用。 如果你通过移除此组的特权来锁定服务器，Analysis Services 可能无法启动，并且将记录此错误：“客户端没有所需的特权。” 此错误发生后，通过将特权授予正确的 Analysis Services 安全组，将特权还原到 Analysis Services。|  
|**调整进程的内存配额** (SeIncreaseQuotaSizePrivilege)|此特权用于当进程因受制于为实例建立的内存阀值而没有足够资源来完成其执行时请求更多内存。|  
|**锁定内存页** (SeLockMemoryPrivilege)|此特权仅在完全关闭分页时所需。 默认情况下，表格服务器实例使用 Windows 分页文件，但您可以通过设置使用 Windows 分页阻止它`VertiPaqPagingPolicy`为 0。<br /><br /> `VertiPaqPagingPolicy` 为 1 （默认值），指示表格服务器实例使用 Windows 分页文件。 分配未锁定，允许 Windows 按需移出分页。 由于正在使用分页，不需要锁定内存页。 因此，对于默认配置 (其中`VertiPaqPagingPolicy`= 1)，不需要授予**锁定内存页**特权仅授予对表格实例。<br /><br /> `VertiPaqPagingPolicy` 为 0。 假定对表格实例授予了 **锁定内存页** 特权，如果关闭 Analysis Services 的分页，则锁定分配。 考虑到此设置和 **锁定内存页** 特权，当系统在内存压力下时，Windows 不能分页出对 Analysis Services 执行的内存分配。 Analysis Services 依赖**锁定内存页**后的强制执行权限`VertiPaqPagingPolicy`= 0。 请注意，不建议关闭 Windows 分页。 它会增加操作的内存不足错误率，而如果允许分页，该操作可能成功。 请参阅[Memory Properties](../server-properties/memory-properties.md)有关详细信息`VertiPaqPagingPolicy`。|  
  
#### <a name="to-view-or-add-windows-privileges-on-the-service-account"></a>若要在服务账户上查看或添加 Windows 特权  
  
1.  请运行“GPEDIT.msc | 本地计算机策略 | 计算机配置 | Windows 设置 | 安全设置 | 本地策略 | 用户权限分配”。  
  
2.  查看现有策略，包括`SQLServerMSASUser$`。 这是在安装 Analysis Services 的计算机上找到的本地安全组。 Windows 特权和文件文件夹权限都授予此安全组。 双击 **作为服务登录** 策略，查看如何在你的系统上指定安全组。 安全组的全名会根据你是否将 Analysis Services 作为命名实例安装而变化。 添加账户特权时，使用此安全组，而不是实际的服务账户。  
  
3.  若要在 GPEDIT 中添加账户特权，右键单击 **“增加进程工作集”** ，然后选择 **“属性”**。  
  
4.  单击 **“添加用户或组”**。  
  
5.  输入 Analysis Services 实例的用户组。 请牢记，服务账户是本地安全组的一个成员，要求你将本地计算机作为账户的域进行预置。  
  
     下表显示有关名为“SQL01-WIN12”的计算机上名为“表格”的默认实例和命名实例的两个示例，其中的计算机名称为本地域。  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$MSSQLSERVER  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$TABULAR  
  
6.  为 **为进程调整内存配额**重复此操作，并选择性地为 **锁定内存页** 或 **提高计划优先级**重复此操作。  
  
> [!NOTE]  
>  旧版安装程序意外将 Analysis Services 服务帐户添加到了 **“Performance Log Users”** 组中。 虽然此缺陷已修复，但现有安装中可能还有这种不必要的组成员身份。 由于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务帐户不需要 **“Performance Log Users”** 组中的成员身份，您可以将其从该组删除。  
  
##  <a name="bkmk_FilePermissions"></a> 分配给 Analysis Services 服务帐户的文件系统权限  
  
> [!NOTE]  
>  有关与每个程序文件夹关联的权限的列表，请参阅 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 。  
>   
>  有关与 IIS 配置和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 相关的文件权限信息，请参阅[在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
 服务器操作所需的所有文件系统权限（包括从指定数据文件夹加载和卸载数据库时所需的权限）均在安装时由 SQL Server 安装程序分配。  
  
 数据文件、程序可执行文件、配置文件、日志文件和临时文件上的权限持有者是由 SQL Server 安装程序创建的一个本地安全组。  
  
 有一个安全组是为你安装的每个实例而创建的。 安全组或者命名实例**SQLServerMSASUser$ MSSQLSERVER**对于默认实例中，或`SQLServerMSASUser$`\<服务器名 >$\<实例名 > 对于命名实例。 该安装程序为此安全组配置执行服务器操作所需的文件权限。 如果您检查 \MSAS12.MSSQLSERVER\OLAP\BIN 目录上的安全权限，则会看到该安全组（而非服务帐户或其 per-service SID）是该目录的权限持有者。  
  
 该安全组仅包含一个成员： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例启动帐户的 per-service 安全标识符 (SID)。 安装程序将 Per-service SID 添加到本地安全组。 与部署 Database Engine 相比， SQL Server 安装程序部署 Analysis Services 小而明显的不同之处在于使用了本地安全组及其 SID 成员身份。  
  
 如果你认为文件权限已损坏，请按照以下步骤来验证服务仍是正确配置的：  
  
1.  使用服务控制命令行工具 (sc.exe) 获取默认服务实例的 SID。  
  
     `SC showsid MSSqlServerOlapService`  
  
     对于命名实例（其中实例名称为 Tabular），请使用以下语法：  
  
     `SC showsid MSOlap$Tabular`  
  
2.  使用**计算机管理器** | **本地用户和组** | **组**检查 SQLServerMSASUser$的成员身份\<服务器名 >$\<实例名 > 安全组。  
  
     成员 SID 应与步骤 1 的 per-service SID 匹配。  
  
3.  使用“计算机管理器”  |  |  |“MSASxx.MSSQLServer”|“”  |  验证是否在步骤 2 中向安全组授予了文件夹安全属性。  
  
> [!NOTE]  
>  切勿删除或修改 SID。 若要还原无意删除的每个服务 SID，请参阅[ http://support.microsoft.com/kb/2620201 ](http://support.microsoft.com/kb/2620201)。  
  
 **了解关于 per-service SID 的详细信息**  
  
 每个 Windows 帐户都有一个关联 [SID](http://en.wikipedia.org/wiki/Security_Identifier)，但服务也可以具有 SID，所以被称为 Per-service SID。 per-service SID 是在安装服务实例时作为服务的唯一且永久附件创建的。 Per-service SID 是从服务名生成的计算机级别的本地 SID。 在默认实例上，用户友好名称是 NT SERVICE\MSSQLServerOLAPService。  
  
 Per-service SID 的优势是其允许任意更改可见范围更广的登录帐户，而不会影响文件权限。 例如，假定您安装了两个 Analysis Services 实例：一个默认实例和一个命名实例，它们在同一 Windows 用户帐户下运行。 共享登录帐户时，每个服务实例都具有唯一 Per-service SID。 此 SID 不同于登录帐户的 SID。 Per-service SID 用于文件权限和 Windows 特权。 与此相反，登陆帐户 SID 用于身份验证和授权方案，即不同的 SID 用于不同目的。  
  
 因为 SID 是不可变的，所以无论你更改服务账户的频率是多少，服务安装时创建的文件系统 ACL 均可无限使用。 作为一项附加的安全措施，通过 SID 指定权限的 ACL 可确保可执行程序和数据文件夹仅由单个服务实例访问，即使同一帐户下运行着其他服务时也如此。  
  
##  <a name="bkmk_tasks"></a> 为特定服务器操作授予附加 Analysis Services 权限  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在用于启动 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的服务帐户（或登录帐户）的安全上下文中执行某些任务，而在发出任务请求的用户的安全上下文中执行另一些任务。  
  
 下表说明了为作为服务帐户运行的任务提供支持所需的其他权限。  
  
|服务器操作|工作项|对齐|  
|----------------------|---------------|-------------------|  
|远程访问外部关系数据源|为服务帐户创建数据库登录名|所谓处理，就是从外部数据源（通常是关系数据库）检索数据，这些数据随后会加载到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中。 用于检索外部数据的凭据选项之一是使用服务帐户。 仅当您为服务帐户创建数据登录名并授予对源数据库的读取权限时，此凭据选项才起作用。 有关如何将服务帐户选项用于此任务的详细信息，请参阅[设置模拟选项（SSAS - 多维）](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md) 。 同样，如果使用 ROLAP 作为存储模式，则可使用相同的模拟选项。 在这种情况下，该帐户还必须对源数据拥有写权限，以便处理 ROLAP 分区（即存储聚合）。|  
|DirectQuery|为服务帐户创建数据库登录名|DirectQuery 是一种表格功能，可使用它来查询以下外部数据集：太大而无法容纳在表格模型中，或具有一些特性使得 DirectQuery 比默认的内存中存储选项更合适。 DirectQuery 模式中可用的一个连接选项是使用服务帐户。 同样，仅当服务帐户具有数据库登录名并拥有对目标数据源的读取权限时，此选项才起作用。 有关如何将服务帐户选项用于此任务的详细信息，请参阅[设置模拟选项（SSAS - 多维）](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md) 。 或者，也可以使用当前用户的凭据来检索数据。 大多数情况下，此选项需要双跃点连接，因此，请确保为服务帐户配置 Kerberos 约束委派，以便服务帐户可以向下游服务器委派标识。 有关详细信息，请参阅 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)。|  
|远程访问其他 SSAS 实例|将服务账户添加到远程服务器上定义的 Analysis Services 数据库角色中|远程分区和引用其他远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的链接对象都是需要对远程计算机或设备拥有权限的系统功能。 当有人员创建并填充远程分区或设置链接对象时，该操作在当前用户的安全上下文中运行。 如果您随后使这些操作自动进行，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在其服务帐户的安全上下文中访问远程实例。 为了访问远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例中的链接对象，登录帐户必须拥有读取远程实例中相应对象的权限，例如，拥有对某些维度的读取权限。 同样，使用远程分区要求服务帐户对远程实例拥有管理权限。 这种权限通过角色在远程 Analysis Services 实例上授予，角色会将允许的操作与特定对象关联起来。 有关如何授予允许处理和查询操作的完全控制权限，请参阅[授予数据库权限 (Analysis Services)](../multidimensional-models/grant-database-permissions-analysis-services.md)。 有关远程分区的信息，请参阅[创建和管理远程分区 (Analysis Services)](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)。|  
|写回|将服务账户添加到远程服务器上定义的 Analysis Services 数据库角色中|写回是可在客户端应用程序中启用的一种多维模型功能，可用来在数据分析期间创建新数据值。 如果在任何维度或多维数据集中启用写回，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务帐户必须对源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据库中的写回表拥有写入权限。 如果该表尚不存在且需要创建，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务帐户还必须在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中拥有创建表的权限。|  
|写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据库中的查询日志表|为服务帐户创建数据库登录名，并分配对查询日志表的写权限|您可以启用查询日志记录将使用情况数据收集在一个数据库表中，以便进行后续分析。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务帐户对指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的查询日志表必须拥有写入权限。 如果该表尚不存在且需要创建，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 登录帐户还必须在指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中拥有创建表的权限。 有关详细信息，请参阅 [通过基于使用情况的优化向导提高 SQL Server Analysis Services 性能（博客）](http://www.mssqltips.com/sqlservertip/2876/improve-sql-server-analysis-services-performance-with-the-usage-based-optimization-wizard/) 和 [Analysis Services 中的查询日志记录（博客）](http://weblogs.asp.net/miked/archive/2013/07/31/query-logging-in-analysis-services.aspx)。|  
  
## <a name="see-also"></a>请参阅  
 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [SQL Server 服务帐户和每个服务 SID （博客）](http://www.travisgan.com/2013/06/sql-server-service-account-and-per.html)   
 [SQL Server 使用服务 SID 来提供服务隔离 （知识库文章）](http://support.microsoft.com/kb/2620201)   
 [访问令牌 (MSDN)](/windows/desktop/SecAuthZ/access-tokens)   
 [安全标识符 (MSDN)](/windows/desktop/SecAuthZ/security-identifiers)   
 [访问令牌 (Wikipedia)](http://en.wikipedia.org/wiki/Access_token)   
 [访问控制列表 (Wikipedia)](http://en.wikipedia.org/wiki/Access_control_list)  
  
  
