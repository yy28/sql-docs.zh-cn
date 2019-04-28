---
title: 创建数据源 (SSAS 多维) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourcedesigner.f1
- sql12.asvs.sqlserverstudio.impersonationinfo.f1
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- impersonation [Analysis Services]
- data sources [Analysis Services], creating
- security [Analysis Services], data source connections
ms.assetid: 9fab8298-10dc-45a9-9a91-0c8e6d947468
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 54971b2b71d37ec4b246d982429fac3d6abf5b9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702156"
---
# <a name="create-a-data-source-ssas-multidimensional"></a>创建数据源（SSAS 多维）
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维模型中，数据源对象表示与您正从其处理（或导入）数据的数据源的连接。 一个多维模型必须包含至少一个数据源对象，但您可以添加更多对象以便合并来自若干数据仓库的数据。 使用本主题中的说明可为您的模型创建数据源对象。 有关在此对象上设置属性的详细信息，请参阅[设置数据源属性（SSAS 多维）](set-data-source-properties-ssas-multidimensional.md)。  
  
 本主题包含以下各节：  
  
 [选择数据访问接口](#bkmk_provider)  
  
 [设置凭据和模拟选项](#bkmk_impersonation)  
  
 [查看或编辑连接属性](#bkmk_ConnectionString)  
  
 [使用数据源向导创建数据源](#bkmk_steps)  
  
 [使用现有连接创建数据源](#bkmk_connection)  
  
 [将多个数据源添加到模型](#bkmk_multipleDS)  
  
##  <a name="bkmk_provider"></a> 选择数据访问接口  
 您可以使用托管的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 或本机 OLE DB 访问接口来进行连接。 SQL Server 数据源的建议的数据访问接口是 SQL Server Native Client，因为它通常提供更好的性能。  
  
 对于 Oracle 和其他第三方数据源，请检查第三方是否提供本机 OLE DB 访问接口，然后首先尝试该访问接口。 如果您遇到错误，请尝试在连接管理器中列出的其他 .NET 访问接口或本机 OLE DB 访问接口之一。 请确保您使用的任何数据访问接口安装在用于开发和运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解决方案的所有计算机上。  
  
##  <a name="bkmk_impersonation"></a> 设置凭据和模拟选项  
 数据源连接有时可以使用 Windows 身份验证或数据库管理系统提供的身份验证服务，例如在连接到 SQL Azure 数据库时使用 SQL Server 身份验证。 您指定的帐户必须能够登录到远程数据库服务器并对外部数据库具有读取权限。  
  
### <a name="windows-authentication"></a>Windows 身份验证  
 使用 Windows 身份验证的连接在数据源设计器的 **“模拟信息”** 选项卡上指定。 使用此选项卡选择在连接到外部数据源时 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 运行所基于的帐户。 并非在所有情况下都可以使用所有选项。 有关这些选项以及何时使用它们的详细信息，请参阅[设置模拟选项（SSAS - 多维）](set-impersonation-options-ssas-multidimensional.md)。  
  
### <a name="database-authentication"></a>数据库身份验证  
 作为对 Windows 身份验证的替代方法，您可以指定使用数据库管理系统提供的身份验证服务的连接。 在某些情况下，需要使用数据库身份验证。 要求使用数据库身份验证的情况包括使用 SQL Server 身份验证连接到 Windows Azure SQL Database，或访问在不同的操作系统上或不受信任的域中运行的关系数据源。  
  
 对于使用数据库身份验证的数据源，在连接字符串上指定数据库登录名的用户名和密码。 当您在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 模型中设置数据源连接时，如果您在连接管理器中输入某一用户名和密码，则凭据将添加到连接字符串中。 请记住，应指定对数据具有读取权限的用户标识。  
  
 在检索数据时，建立连接的客户端库将形成在连接字符串中包括凭据的连接请求。 “模拟信息”选项卡中的 Windows 身份验证凭据选项不用于该连接，但可用于其他操作，例如访问本地计算机上的资源。 有关详细信息，请参阅[设置模拟选项（SSAS - 多维）](set-impersonation-options-ssas-multidimensional.md)。  
  
 在您的模型中保存数据源对象后，对连接字符串和密码进行加密。  出于安全目的，当您随后在工具、脚本或代码中查看密码时，密码的所有可见痕迹都将从连接字符串中删除。  
  
> [!NOTE]  
>  默认情况下， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 不会将密码与连接字符串一起保存。 如果未保存密码，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在需要密码时提示您输入密码。 如果选择保存密码，则密码以加密格式存储在数据连接字符串中。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用包含数据源的数据库的数据库加密密钥加密该数据源的密码信息。 对连接信息进行加密之后，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器更改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务帐户或密码，否则无法恢复加密的信息。 有关详细信息，请参阅 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)。  
  
### <a name="defining-impersonation-information-for-data-mining-objects"></a>为数据挖掘对象定义模拟信息  
 数据挖掘查询可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务帐户的上下文中执行，但是还可以在提交此查询的用户的上下文中执行，也可以在指定用户的上下文中执行。 执行查询所在的上下文可能会影响查询结果。 对于数据挖掘 `OPENQUERY` 类型操作，您可能希望数据挖掘查询在当前用户的上下文中执行或在指定用户（无论此用户是否执行此查询）的上下文中执行，而不是在服务帐户的上下文中执行。 这使得查询使用受限安全凭据执行。 如果您希望 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 模拟当前用户或模拟指定用户，则请选择 **“使用特定用户名和密码”** 选项或 **“使用当前用户的凭据”** 选项。  
  
##  <a name="bkmk_steps"></a> 使用数据源向导创建数据源  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开要在其中定义数据源的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或连接到要在其中定义数据源的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
2.  在“解决方案资源管理器”中，右键单击“数据源”文件夹，然后单击“新建数据源”以便启动“数据源向导”。  
  
3.  在 **“选择如何定义连接”** 页中，选择 **“基于现有连接或新连接创建数据源”** ，然后单击 **“新建”** 以便打开 **“连接管理器”**。  
  
     在连接管理器中创建新连接。 在连接管理器中，选择一个访问接口，然后指定由该访问接口用来连接到基础数据的连接字符串属性。 所需的确切信息取决于选定的访问接口，但通常此类信息包括某个服务器或服务实例、登录到该服务器或服务实例所用的信息、数据库或文件名以及访问接口的其他特定设置。 对于此过程的其余部分，我们假定 SQL Server 数据库连接。  
  
4.  选择要用于该连接的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 或本机 OLE DB 访问接口。  
  
     新连接的默认访问接口是“本机 OLE DB\\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client”访问接口。 此访问接口用于连接到使用 OLE DB 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎实例。 要连接到 SQL Server 关系数据库，使用 Native OLE DB\SQL Server Native Client 11.0 通常要比使用备用访问接口要快。  
  
     您可以选择一个不同的访问接口来访问其他数据源。 有关提供程序和关系数据库支持的一系列[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，请参阅[支持数据源&#40;SSAS 多维&#41;](supported-data-sources-ssas-multidimensional.md)。  
  
5.  输入选定访问接口连接到基础数据源所需的信息。 如果选中“本机 OLE DB\SQL Server Native Client”访问接口，请输入以下信息：  
  
    1.  **“服务器名称”** 是数据库引擎实例的网络名称。 它可以指定为 IP 地址、计算机的 NETBIOS 名称或完全限定域名。 如果服务器作为命名实例安装，则必须包括实例名称 (例如，\<计算机名 >\\< 实例名\>)。  
  
    2.  **“登录到服务器”** 指定将对连接进行身份验证的方式。 **“使用 Windows 身份验证”** 使用 Windows 身份验证。 **“使用 SQL Server 身份验证”** 为支持混合模式身份验证的 Windows Azure SQL Database 或 SQL Server 实例指定数据库用户登录名。  
  
        > [!IMPORTANT]  
        >  连接管理器对于使用 SQL Server 身份验证的连接包括一个 **“保存我的密码”** 复选框。 尽管显示此复选框，但并不总是使用它。  
        >   
        >  在 Analysis Services 不使用此复选框的情况下，此时将包括刷新或处理在活动 Analysis Services 数据库中使用的 SQL Server 关系数据。 无论您是清除还是选中 **“保存我的密码”**，Analysis Services 始终将加密和保存密码。 密码加密后同时存储在 .abf 和数据文件中。 之所以存在此行为，是因为 Analysis Services 不支持在服务器上存储基于会话的密码。  
        >   
        >  此行为仅适用于满足以下条件的数据库：a) 在 Analysis Services 服务器实例上持久存在；b) 使用 SQL Server 身份验证刷新或处理关系数据。 它确实不适用于您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中设置的专用于会话期间的数据源连接。 尽管无法删除已经存储的密码，但您可以使用不同的凭据或 Windows 身份验证来覆盖当前随数据库存储的用户信息。  
  
    3.  **“选择或输入数据库名称”** 或 **“附加一个数据库文件”** 用于指定数据库。  
  
    4.  在此对话框的左侧，单击 **“全部”** 可查看此连接的其他设置，其中包括此访问接口的所有默认设置。  
  
    5.  根据环境需要更改设置并单击 **“确定”**。  
  
         将在数据源向导的 **“选择如何定义连接”** 页的 **“数据连接”** 窗格中显示新连接。  
  
6.  单击“下一步” 。  
  
7.  在 **“模拟信息”** 中，指定在连接到外部数据源时 Analysis Services 将使用的 Windows 凭据或用户标识。 如果您正在使用数据库身份验证，则出于连接目的，这些设置将被忽略。  
  
     用于选择模拟选项的准则因您使用数据源的方式而异。 对于处理任务， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务在连接到数据源时，必须在其服务帐户或指定用户帐户的安全上下文中运行。  
  
    -   **“使用特定 Windows 用户名和密码”** 将指定一组唯一的最小权限凭据。  
  
    -   **“使用服务帐户”** 将使用服务标识处理数据。  
  
     您指定的帐户必须对数据源具有读取权限。  
  
8.  单击“下一步” 。  在 **“完成向导”** 中，输入数据源名称或使用默认名称。 默认名称是在连接中指定的数据库的名称。 **“预览”** 窗格将显示此新数据源的连接字符串。  
  
9. 单击 **“完成”**。  此时，解决方案资源管理器的 **“数据源”** 文件夹中将出现新数据源。  
  
##  <a name="bkmk_connection"></a> 使用现有连接创建数据源  
 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时，您的数据源可以基于解决方案中的现有数据源，也可以基于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 数据源向导提供了几个用于创建数据源对象的选项，包括在同一个项目中使用现有连接。  
  
-   基于解决方案中的现有数据源创建数据源之后，您可以定义与现有数据源同步的数据源。 生成包含该新数据源的项目时，将使用基础数据源中的数据源设置。  
  
-   基于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目创建数据源之后，您可以在当前项目中引用解决方案中的其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 新的数据源使用 MSOLAP 访问接口，并且该数据源的 `Data Source` 属性和 `Initial Catalog` 属性从选定项目的 `TargetServer` 属性和 `TargetDatabase` 属性获取。 在使用多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目管理远程分区的解决方案中，因为源和目标 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库需要互逆数据源来支持远程分区存储和处理，所以该功能很有用。  
  
 在引用数据源对象时，只能在被引用对象或项目中编辑此对象。 不能在包含该引用的数据源对象中编辑连接信息。 在被引用对象或项目中对连接信息的更改会显示在生成后的新数据源中。 在生成项目或在数据源设计器中清除引用时，显示在项目的数据源 (.ds) 文件中的连接字符串信息将被同步。  
  
##  <a name="bkmk_ConnectionString"></a> 查看或编辑连接属性  
 连接字符串基于您在数据源设计器或新建数据源向导中选择的属性构成。 您可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中查看连接字符串和其他属性。  
  
 **编辑连接字符串**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的解决方案资源管理器中双击数据源对象。  
  
2.  单击 **“编辑”**，然后在左侧的导航窗格中单击 **“所有”** 。  
  
3.  属性网格将出现，其中显示您正在使用的数据访问接口的可用属性。 有关这些属性的详细信息，请参阅访问接口的产品文档。  对于 SQL Server 本机客户端，请参阅 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 如果解决方案中具有多个数据源，并且您希望在同一位置维护连接字符串，则可以将当前数据源配置为引用其他数据源对象。  
  
 “数据源引用”  是与同一解决方案中的其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象或数据源之间的关联。 引用提供了一种在解决方案的对象之间同步数据源的方式。 每次生成项目时，都会同步连接字符串信息。 若要更改引用另一对象的数据源的连接字符串，则必须更改被引用对象的连接字符串。  
  
 您可以通过清除此复选框来删除该引用。 此操作将结束对象间的同步并允许您更改数据源中的连接字符串。  
  
##  <a name="bkmk_multipleDS"></a> 将多个数据源添加到模型  
 您可以创建多个数据源对象，以便支持与其他数据源的连接。 每个数据源都必须具有可以用来创建关系的列。  
  
> [!NOTE]  
>  如果定义了多个数据源和从单个查询中的多个源查询数据，例如对于雪花型维度，则必须定义支持使用远程查询的数据源`OpenRowset`。 通常，此数据源将为 Microsoft SQL Server 数据源。  
  
 使用多个数据源的要求包括：  
  
-   将一个数据源指定主数据源。 主数据源是用于创建数据源视图的数据源。  
  
-   主数据源必须支持 `OpenRowset` 函数。   有关 SQL Server 中该函数的详细信息，请参阅 <xref:Microsoft.SqlServer.TransactSql.ScriptDom.TSqlTokenType.OpenRowSet>。  
  
 使用以下方法可合并来自多个数据源的数据：  
  
1.  在模型中创建数据源。  
  
2.  创建数据源视图，使用 SQL Server 关系数据库作为数据源。 这是您的主数据源。  
  
3.  在数据源视图设计器中，使用刚创建的数据源视图，在工作区的任何地方右键单击，然后选择“添加/删除表”。  
  
4.  选择第二个数据源，然后选择您要添加的表。  
  
5.  查找并选择您所添加的表。 右键单击该表，然后选择“新建关系”。 选择包含匹配数据的源列和目标列。  
  
## <a name="see-also"></a>请参阅  
 [支持的数据源&#40;SSAS 多维&#41;](supported-data-sources-ssas-multidimensional.md)   
 [多维模型中的数据源视图](data-source-views-in-multidimensional-models.md)  
  
  
