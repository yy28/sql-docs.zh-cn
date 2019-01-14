---
title: dtexec 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d30dbae5ffe7a392fc846b575a44af66246c9682
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132767"
---
# <a name="dtexec-utility"></a>dtexec 实用工具
  `dtexec`命令提示实用工具用于配置和执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包。 使用 `dtexec` 实用工具，可以访问所有包配置和执行功能，如参数、连接、属性、变量、日志和进度指示器等。 `dtexec`实用工具，可以加载来自以下源的包：[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服务器、.ispac 项目文件， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，[!INCLUDE[ssIS](../../includes/ssis-md.md)]包存储区和文件系统。  
  
> [!NOTE]  
>  当使用 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] 附带的 `dtexec` 实用工具版本运行 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 或 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会临时将该包升级到 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]。 不过，您不能使用 `dtexec` 实用工具保存这些升级的更改。 有关如何向包永久地升级的详细信息[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]，请参阅[升级 Integration Services 包](../install-windows/upgrade-integration-services-packages.md)。  
  
 本主题包含以下各节：  
  
-   [Integration Services 服务器和项目文件](#server)  
  
-   [64 位计算机上的安装注意事项](#bit)  
  
-   [有关使用并行安装的计算机的注意事项](#side)  
  
-   [执行的阶段](#phases)  
  
-   [返回的退出代码](#exit)  
  
-   [语法规则](#syntaxRules)  
  
-   [从 xp_cmdshell 中使用 dtexec](#cmdshell)  
  
-   [语法](#syntax)  
  
-   [Parameters](#parameter)  
  
-   [注释](#remark)  
  
-   [示例](#example)  
  
##  <a name="server"></a> Integration Services 服务器和项目文件  
 当你使用`dtexec`上运行包[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服务器，`dtexec`调用[catalog.create_execution &#40;SSISDB 数据库&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database)， [catalog.set_execution_parameter_值&#40;SSISDB 数据库&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)并[catalog.start_execution &#40;SSISDB 数据库&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)存储的过程来创建一个执行、 设置参数值并启动执行。 可以在服务器的相关视图中或使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中提供的标准报告来查看所有执行日志。 有关报表的详细信息，请参阅 [Integration Services 服务器的报表](../reports-for-the-integration-services-server.md)。  
  
 以下是在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上执行包的一个示例。  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 使用 `dtexec` 从 .ispac 项目文件运行包时，相关选项 /Proj[ect] 和 /Pack[age] 用于指定项目路径和包流名称。 通过从 **运行** “Integration Services 项目转换向导” [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]将项目转换为项目部署模型时，该向导生成一个 .ispac 项目文件。 有关详细信息，请参阅 [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md)。  
  
 可以使用`dtexec`与第三方计划工具来计划到部署包的[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服务器。  
  
##  <a name="bit"></a> 64 位计算机上的安装注意事项  
 在 64 位计算机上，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将安装 64 位版本的 `dtexec` 实用工具 (dtexec.exe)。 如果需要以 32 位模式运行某些包，则必须安装 32 位版本的 `dtexec` 实用工具。 若要安装 32 位版本的 `dtexec` 实用工具，必须在安装过程中选择“客户端工具”或 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]。  
  
 默认情况下，同时安装了 64 位和 32 位版本的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 命令提示实用工具的 64 位计算机将在命令提示符处运行 32 位版本。 运行 32 位版本的原因是：在 PATH 环境变量中，32 位版本的目录路径显示在 64 位版本的目录路径之前。 （通常，32 位目录路径是 \<drive>:\Program Files(x86)\Microsoft SQL Server\110\DTS\Binn，而 64 位目录路径是\<drive>:\Program Files\Microsoft SQL Server\110\DTS\Binn。）  
  
> [!NOTE]  
>  如果使用 SQL Server 代理来运行此实用工具，则 SQL Server 代理会自动使用 64 位版本的实用工具。 SQL Server 代理使用注册表（而非 PATH 环境变量）来找到此实用工具的正确可执行文件。  
  
 若要确保在命令提示符处运行 64 位版本的实用工具，可以执行以下操作之一：  
  
-   打开命令提示符窗口，更改为包含 64 位版本的实用工具的目录 (\<drive>:\Program Files\Microsoft SQL Server\110\DTS\Binn)，然后从该位置运行此实用工具。  
  
-   在命令提示符处，通过输入 64 位版本的实用工具的完整路径 (\<drive>:\Program Files\Microsoft SQL Server\110\DTS\Binn) 来运行此实用工具。  
  
-   通过将 64 位路径 (\<drive>:\Program Files\Microsoft SQL Server\110\DTS\Binn) 置于 32 位路径 (\<drive>:\ Program Files(x86)\Microsoft SQL Server\110\DTS\Binn) 之前，可永久更改 PATH 环境变量中路径的顺序。  
  
##  <a name="side"></a> 有关使用并行安装的计算机的注意事项  
 当在已安装 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 或 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 的计算机上安装 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 时，安装多个版本的 `dtexec` 实用工具。  
  
 若要确保运行正确的实用工具版本，请在命令提示符处，通过输入完整路径 (\<drive>:\Program Files\Microsoft SQL Server\\<version\>\DTS\Binn) 来运行此实用工具。  
  
##  <a name="phases"></a> 执行的阶段  
 该实用工具的执行过程经历四个阶段。 这些阶段如下所列：  
  
1.  命令选项确定阶段：命令提示符读取选项列表和已指定的参数。 如果遇到 **/?** 或 **/HELP** 选项，则会跳过所有后续阶段。  
  
2.  包加载阶段：指定的包`/SQL`， **/file**，或`/DTS`加载选项。  
  
3.  配置阶段：按以下顺序处理各个选项：  
  
    -   设置包标志、变量和属性的选项。  
  
    -   验证包版本和内部版本的选项。  
  
    -   配置实用工具运行时行为（如报告）的选项。  
  
4.  验证和执行阶段：运行，或如果验证但不运行包 **/validate**指定选项。  
  
##  <a name="exit"></a> 返回的退出代码  
 **dtexec 实用工具返回的退出代码**  
  
 运行包时，`dtexec` 可能会返回退出代码。 使用该退出代码填充 ERRORLEVEL 变量，然后可以在批处理文件的条件语句或分支逻辑中测试该变量的值。 下表列出了 `dtexec` 实用工具退出时可以设置的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0|已成功执行包。|  
|1|包失败。|  
|3|用户取消了包。|  
|4|实用工具找不到请求的包。 无法找到包。|  
|5|实用工具无法加载请求的包。 无法加载包。|  
|6|实用工具的命令行中有内部语法错误或语义错误。|  
  
##  <a name="syntaxRules"></a> 语法规则  
 **实用工具语法规则**  
  
 所有选项必须以斜杠 (/) 或减号 (-) 开头。 此处显示的选项以斜杠 (/) 开始，但可用减号 (-) 替换。  
  
 如果参数包含空格，则必须用引号将该参数引起来。 如果没有使用引号将参数引起来，则该参数不能包含空格。  
  
 用引号引起来的字符串中的双引号表示转义单引号。  
  
 除密码外，其他选项和参数都不区分大小写。  
  
##  <a name="cmdshell"></a> 从 xp_cmdshell 中使用 dtexec  
 **从 xp_cmdshell 中使用 dtexec**  
  
 可以从 **xp_cmdshell** 提示符处运行 dtexec。 以下示例显示如何运行名为 UpsertData.dtsx 的包并忽略返回代码：  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 以下示例显示如何运行相同的包并捕获返回代码：  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> [!IMPORTANT]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，新安装中将默认禁用 **xp_cmdshell** 选项。 运行 **sp_configure** 系统存储过程可以启用此选项。 有关详细信息，请参阅 [xp_cmdshell 服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
##  <a name="syntax"></a> 语法  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameter"></a> Parameters  
  
-   **/?** [*option_name*]:可选。 显示命令提示符选项，或显示指定的 *option_name* 的帮助，然后关闭实用工具。  
  
     如果指定*option_name*自变量，`dtexec`启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书并显示 dtexec 实用工具主题。  
  
-   **/Ca [llerInfo]**:   
                  可选。 指定有关包执行的其他信息。 使用 SQL Server 代理运行包时，代理设置此参数以指示包执行由 SQL Server 代理调用。 从命令行运行 `dtexec` 实用工具时，忽略此参数。  
  
-   **/Checkf [ile]** _filespec_:   
                  可选。 集`CheckpointFileName`包中的路径和文件名指定的属性*filespec*。 重新启动包时将使用此文件。 如果指定了该选项并且未提供文件名值，则包的 `CheckpointFileName` 将被设置为空字符串。 如果不指定该选项，则保留包中的值。  
  
-   **/Checkp [ointing]** _{on\off}_:   
                  可选。 设置一个值，用于确定包执行期间包是否使用检查点。 值 **on** 指定要重新运行失败的包。 重新运行失败的包时，运行时引擎将使用检查点文件，以便从失败点重新启动包。  
  
     如果声明该选项时未提供值，则默认值为“on”。 如果值设置为“on”，但找不到检查点文件，则包执行将失败。 如果不指定该选项，则保留包中设置的值。 有关详细信息，请参阅 [通过使用检查点重新启动包](restart-packages-by-using-checkpoints.md)。  
  
     **上的 /CheckPointing** dtexec 选项等效于设置`SaveCheckpoints`为 True 时，包的属性和`CheckpointUsage`属性为始终。  
  
-   **/Com [mandFile]** _filespec_:   
                  （可选）。 指定要使用 `dtexec` 运行的命令选项。 打开 *filespec* 中指定的文件，并读取该文件中的选项，直到在文件中找到 EOF。 *filespec* 是一个文本文件。 *filespec* 参数指定与包执行关联的命令文件的文件名和路径。  
  
-   **/Conf [igFile]** _filespec_:可选。 指定要从中提取值的配置文件。 使用该选项，可以设置一个与设计包时指定的配置不同的运行时配置。 可以将不同的配置设置存储在 XML 配置文件中，然后在执行包之前使用 **/ConfigFile** 选项加载这些设置。  
  
     可以使用 **/ConfigFile** 选项在运行时加载在设计时未指定的其他配置。 不过，不能使用 **/ConfigFile** 选项来替换在设计时也指定了的配置值。 若要了解如何应用包配置，请参阅 [Package Configurations](../package-configurations.md)。  
  
-   **/Conn [ection]** _id_or_name; connection_string [[; id_or_name; connection_string]...]_:   
                  可选。 指定带有指定名称或 GUID 的连接管理器位于包中，并指定了连接字符串。  
  
     该选项要求同时指定两个参数：必须在 *id_or_name* 参数中提供连接管理器名称或 GUID，并且在 *connection_string* 参数中指定有效的连接字符串。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](../connection-manager/integration-services-ssis-connections.md)。  
  
     在运行时，可以使用 **/Connection** 选项从在设计时指定的位置之外的某个位置加载包配置。 这些配置的值随后将替换最初指定的值。 不过，可以将 **/Connection** 选项仅用于使用连接管理器的配置，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置。 若要了解如何应用包配置，请参阅[包配置](../package-configurations.md)并[SQL Server 2014 中 Integration Services 功能的行为更改](../behavior-changes-to-integration-services-features-in-sql-server-2014.md)。  
  
-   **/Cons [oleLog]** [[*displayoptions*]; [*list_options*;*src_name_or_guid*]...]:可选。 在包执行过程中，在控制台显示指定的日志项。 如果省略该选项，则不会在控制台中显示日志项。 如果指定该选项时不带限制显示的参数，则会显示所有日志项。 若要限制控制台显示的日志项，可以使用 *displayoptions* 参数指定要显示的列，并使用 *list_options* 参数限制日志项类型。  
  
    > [!NOTE]  
    >  上运行包时[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]通过使用服务器`/ISSERVER`参数，控制台输出是受限，大多数 **/cons [oleLog]** 选项不适用。 可以在服务器的相关视图中或使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中提供的标准报告来查看所有执行日志。 有关报表的详细信息，请参阅 [Integration Services 服务器的报表](../reports-for-the-integration-services-server.md)。  
  
     *displayoptions* 值包括：  
  
    -   N（名称）  
  
    -   C（计算机）  
  
    -   O（操作员）  
  
    -   S（源名称）  
  
    -   G（源 GUID）  
  
    -   X（执行 GUID）  
  
    -   M（消息）  
  
    -   T（开始和结束时间）  
  
     *list_options* 值包括：  
  
    -   *I* — 指定包含列表。 仅记录指定的源名称或 GUID。  
  
    -   *E* — 指定排除列表。 不记录指定的源名称或 GUID。  
  
    -   为包含或排除指定的 *src_name_or_guid* 参数是事件名称、源名称或源 GUID。  
  
     如果在同一个命令提示符中使用多个 **/ConsoleLog** 选项，它们的相互影响如下：  
  
    -   它们的出现顺序没有影响。  
  
    -   如果命令行中不存在包含列表，将对所有类型日志项应用排除列表。  
  
    -   如果命令行中存在包含列表，将对所有包含列表统一应用排除列表。  
  
     有关的示例 **/ConsoleLog**选项，请参阅**备注**部分。  
  
-   **/D [ts]** _package_path_:   
                  可选。 从 SSIS 包存储区加载包。 使用旧的包部署模型部署存储在 SSIS 包存储区中的包。 若要使用项目部署模型运行部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的包，请使用 `/ISServer` 选项。 有关包和项目部署模型的详细信息，请参阅 [Deployment of Projects and Packages](deploy-integration-services-ssis-projects-and-packages.md)。  
  
     *package_path* 参数指定 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包的相对路径，从 SSIS 包存储的根目录开始，包括 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包的名称。 如果 *package_path* 参数中指定的路径或文件名包含空格，则必须在 *package_path* 参数两侧加上引号。  
  
     `/DTS` 选项不能与 `/File` 或 `/SQL` 选项一起使用。 如果指定多个选项，`dtexec` 将失败。  
  
-   **/De [crypt]**_密码_:  可选。 设置加载使用密码加密的包时所用的解密密码。  
  
-   **/Dump** _错误代码_:  
                  可选创建调试转储文件.mdmp 和.tmp，在包运行期间发生一个或多个指定的事件时。 error code 参数指定将触发系统创建调试转储文件的事件代码类型：错误、警告或信息。 若要指定多个事件代码，请用分号 (;) 分隔每个 *error code* 参数。 不要对 *error code* 参数使用引号。  
  
     以下示例在发生 DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER 错误时生成调试转储文件。  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     默认情况下[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]将调试转储文件存储在文件夹中， *\<驱动器 >*: \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps。  
  
    > [!NOTE]  
    >  调试转储文件可能包含敏感信息。 使用访问控制列表 (ACL) 来限制对这些文件的访问，或将文件复制到具有受限访问权限的文件夹中。 例如，在将调试文件发送给 Microsoft 支持服务部门之前，建议您删除所有敏感信息或机密信息。  
  
     若要将此选项应用到所有包，`dtexec`实用工具运行，添加**DumpOnCodes** REG_SZ 值到 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath 注册表项。 **DumpOnCodes** 中的数据值指定将触发系统创建调试转储文件的错误代码或代码。 多个错误代码必须以分号 (;) 分隔。  
  
     如果将 **DumpOnCodes** 值添加到注册表项，并使用 **/Dump** 选项，系统将创建基于这两个设置的调试转储文件。  
  
     有关调试转储文件的详细信息，请参阅 [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md)。  
  
-   **/Dumponerror**:   
                  可选。 包运行期间出现任意错误时将创建调试转储文件.mdmp 和.tmp。  
  
     默认情况下，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将调试转储文件存储在 \<drive>:\Program Files\Microsoft SQL Server\110\Shared\ErrorDumps 文件夹中。  
  
    > [!NOTE]  
    >  调试转储文件可能包含敏感信息。 使用访问控制列表 (ACL) 来限制对这些文件的访问，或将文件复制到具有受限访问权限的文件夹中。 例如，在将调试文件发送给 Microsoft 支持服务部门之前，建议您删除所有敏感信息或机密信息。  
  
     若要将此选项应用到所有包，`dtexec`实用工具运行，添加**DumpOnError** REG_DWORD 值到 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath 注册表项。 值**DumpOnError** REG_DWORD 值决定是否 **/DumpOnError**选项需与一起使用`dtexec`实用程序：  
  
    -   非零数据值指示出现任意错误，而不管你使用时，系统将创建调试转储文件 **/DumpOnError**选项与`dtexec`实用程序。  
  
    -   零数据值指示，系统将不会创建调试转储文件除非使用 **/DumpOnError**选项与`dtexec`实用程序。  
  
     有关调试转储文件的详细信息，请参阅 [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md)。  
  
-   `/Env[Reference]` *环境引用 ID*:   
                  可选。 为部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的包指定包执行使用的环境引用 (ID)。 配置为绑定到变量的参数将使用环境中包含的变量值。  
  
     可以将 `/Env[Reference]` 选项与 `/ISServer` 和 `/Server` 选项一起使用。  
  
     此参数由 SQL Server 代理使用。  
  
-   **/F [ile]** _filespec_:   
                  可选。 加载保存在文件系统中的包。 使用旧的包部署模型部署保存在文件系统中的包。 若要使用项目部署模型运行部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的包，请使用 `/ISServer` 选项。 有关包和项目部署模型的详细信息，请参阅 [Deployment of Projects and Packages](deploy-integration-services-ssis-projects-and-packages.md)。  
  
     *filespec* 参数指定包的路径和文件名。 可以将路径指定为通用命名约定 (UNC) 路径或本地路径。 如果 *filespec* 参数中指定的路径或文件名包含空格，则必须在 *filespec* 参数两侧加上引号。  
  
     `/File` 选项不能与 `/DTS` 或 `/SQL` 选项一起使用。 如果指定多个选项，`dtexec` 将失败。  
  
-   **/H [elp]** [*option_name*]:可选。 显示选项的帮助，或显示指定的 *option_name* 的帮助，同时关闭实用工具。  
  
     如果指定*option_name*自变量，`dtexec`启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书并显示 dtexec 实用工具主题。  
  
-   `/ISServer` *packagepath*:  
                  可选。 运行部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的包。 *PackagePath* 参数指定部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的包的完整路径和文件名。 如果 *PackagePath* 参数中指定的路径或文件名包含空格，则必须在 *PackagePath* 参数两侧加上引号。  
  
     包格式如下所示：  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     可以将 `/Server` 选项与 `/ISSERVER` 选项一起使用。 只有 Windows 身份验证可以在 SSIS 服务器上执行包。 当前 Windows 用户用于访问该包。 如果省略 /Server 选项，则假定使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认本地实例。  
  
     `/ISSERVER` 选项不能与 `/DTS`、`/SQL` 或 `/File` 选项一起使用。 如果指定多个选项，dtexec 将失败。  
  
     此参数由 SQL Server 代理使用。  
  
-   **/L [ogger]** _classid_orprogid; configstring_:  
                  可选。 将一个或多个日志提供程序与 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包的执行关联。 *classid_orprogid* 参数指定日志提供程序，可以指定为类 GUID。 *configstring* 是用于配置日志提供程序的字符串。  
  
     以下列表显示了可用的日志提供程序：  
  
    -   文本文件：  
  
        -   ProgID：DTS.LogProviderTextFile.1  
  
        -   ClassID：{59B2C6A5-663F-4C20-8863-C83F9B72E2EB}  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]设置用户帐户 ：  
  
        -   ProgID：DTS.LogProviderSQLProfiler.1  
  
        -   ClassID：{5C0B8D21-E9AA-462E-BA34-30FF5F7A42A1}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]设置用户帐户 ：  
  
        -   ProgID：DTS.LogProviderSQLServer.1  
  
        -   ClassID：{6AA833A1-E4B2-4431-831B-DE695049DC61}  
  
    -   Windows 事件日志：  
  
        -   ProgID：DTS.LogProviderEventLog.1  
  
        -   ClassID：{97634F75-1DC7-4F1F-8A4C-DAF0E13AAA22}  
  
    -   XML 文件：  
  
        -   ProgID：DTS.LogProviderXMLFile.1  
  
        -   ClassID：{AFED6884-619C-484F-9A09-F42D56E1A7EA}  
  
-   **/M [axConcurrent]** _concurrent_executables_:  
                  可选。 指定包可以同时执行的可执行文件数。 指定的值必须是非负整数或 -1。 如果值为 -1，则表示 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 所允许的最大并发运行可执行文件数等于执行包的计算机上的处理器总数加二。  
  
-   **/Pack [age]** _PackageName_:  
                  可选。 指定执行的包。 当从 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]执行包时，主要使用此参数。  
  
-   **/P [assword]** _密码_:  
                  可选。 允许检索受 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证保护的包。 该选项与 **/User** 选项一起使用。 如果省略 **/Password** 选项但使用 **/User** 选项，则使用空白密码。 *password* 值可以用引号引起来。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par [ameter]** [$Package:: | $Project:: | $ServerOption::] *parameter_name* [(data_type)];*literal_value*:可选。 指定参数值。 可以指定多个 **/Parameter** 选项。 数据类型是作为字符串的 CLR TypeCodes。 对于非字符串参数，在括号中指定数据类型，前面接着参数名称。  
  
     **/Parameter**选项可仅与`/ISServer`选项。  
  
     使用 $Package、$Project 和 $ServerOption 前缀分别指示包参数、项目参数和服务器选项参数。 默认参数类型为包。  
  
     以下示例执行一个包并为项目参数 (myparam) 提供 myvalue 以及为包参数 (anotherparam) 提供整数值 12。  
  
     `Dtexec /isserver "SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "." /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     您还可以通过使用参数设置连接管理器属性。 可以使用 CM 前缀来表示连接管理器参数。  
  
     在以下示例中，将 SourceServer 连接管理器的 InitialCatalog 属性设置为 `ssisdb`。  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     在以下示例中，将 SourceServer 连接管理器的 ServerName 属性设置为一个句点 (.)，用来指示本地服务器。  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj [ect]** _ProjectFile_:  
                  可选。 指定从中检索执行的包的项目。 *ProjectFile* 参数指定 .ispac 文件名。 当从 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]执行包时，主要使用此参数。  
  
-   **/Rem** _注释_:  
                  可选。 在命令提示符或命令文件中包含注释。 该参数可选。 *comment* 的值是字符串，必须用引号引起来或不含空格。 如果未指定参数，将插入一个空行。 命令选项确定阶段，将放弃*comment* 值。  
  
-   **/Rep [orting]** _级别_[*; event_guid_or_name*[*; event_guid_or_name*[...]]:可选。 指定要报告的消息类型。 *level* 可用的报告选项如下：  
  
     **N** 无报告。  
  
     `E` 将报告错误。  
  
     **W** 报告警告。  
  
     `I` 报告信息性消息。  
  
     **C** 报告自定义事件。  
  
     **D** 报告数据流任务事件。  
  
     **P** 报告进度。  
  
     **V** 详细报告。  
  
     V 和 N 参数与所有其他参数互相排斥，必须单独指定。 如果 **/Reporting**则默认级别为未指定选项`E`（错误）、 **W** （警告） 和**P** （进度）。  
  
     所有事件前都有一个格式为“YY/MM/DD HH:MM:SS”的时间戳以及一个 GUID 或友好名称（如果可用）。  
  
     可选参数 *event_guid_or_name* 是日志提供程序的异常列表。 该异常指定本应记录但却未记录的事件。  
  
     如果默认情况下通常不记录某个事件，则不必排除该事件。  
  
-   **/Res [tart]** {*deny | force | ifPossible*}:可选。 为包的 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 属性指定新值。 各参数的含义如下：  
  
     *Deny* 将 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 属性设置为 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>。  
  
     *Force* 将 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 属性设置为 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>。  
  
     *ifPossible* 将 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 属性设置为 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>。  
  
     如果不指定值，则使用默认值 **force** 。  
  
-   **/Set** [$Sensitive::]*propertyPath; 值*:可选。 覆盖包中参数、变量、属性、容器、日志提供程序、Foreach 枚举器或连接的配置。 使用该选项时， **/Set** 可将 *propertyPath* 参数更改为指定的值。 可以指定多个 **/Set** 选项。  
  
     除了使用之外 **/set**选项与 **/F [ile]** 选项，也可以使用 **/set**选项与`/ISServer`选项或`/Project`选项。 当你使用 **/set**与`/Project`， **/set**设置参数值。 当你使用 **/set**与`/ISServer`， **/set**设置属性覆盖。 此外，使用 **/set**与`/ISServer`，可以使用可选的 $Sensitive 前缀来指示，该属性应被视为区分上[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服务器。  
  
     可以通过运行包配置向导确定 *propertyPath* 的值。 选定项的路径会显示在最后一个 **“完成向导”** 页中，可以进行复制和粘贴。 如果仅以此目的使用该向导，则可以在复制路径后取消它。  
  
     以下示例执行文件系统中保存的包并为变量提供新值：  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     以下示例从 .ispac 项目文件运行包并设置包参数和项目参数。  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     可以使用 **/Set** 选项更改自其加载包配置的位置。 但是，不能使用 **/Set** 选项覆盖设计时某个配置所指定的值。 若要了解如何应用包配置，请参阅[包配置](../package-configurations.md)并[SQL Server 2014 中 Integration Services 功能的行为更改](../behavior-changes-to-integration-services-features-in-sql-server-2014.md)。  
  
-   `/Ser[ver]` *服务器*:  
                  可选。 指定了 `/SQL` 或 `/DTS` 选项时，此选项可以指定从中检索包的服务器的名称。 如果省略 `/Server` 选项并指定 `/SQL` 或 `/DTS` 选项，则尝试对本地服务器执行包。 *server_instance* 值可以用引号引起来。  
  
     指定 `/Ser[ver]` 选项时，必须指定 `/ISServer` 选项。  
  
-   **/SQ [L]** _package_path_:  
                  加载存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 `msdb` 数据库中的包。 使用包部署模型部署存储在 `msdb` 数据库中的包。 若要使用项目部署模型运行部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的包，请使用 `/ISServer` 选项。 有关包和项目部署模型的详细信息，请参阅 [Deployment of Projects and Packages](deploy-integration-services-ssis-projects-and-packages.md)。  
  
     *package_path* 参数指定要检索的包的名称。 如果文件夹包含在路径中，则文件夹将以反斜杠（“\\”）结束。 *package_path* 值可以用引号引起来。 如果 *package_path* 参数中指定的路径或文件名包含空格，则必须在 *package_path* 参数两侧加上引号。  
  
     可以使用 **/User**， **/Password**，并`/Server`选项一起使用`/SQL`选项。  
  
     如果省略 **/User** 选项，则使用 Windows 身份验证来访问包。 如果使用 **/User** 选项，指定的 **/User** 登录名将与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证相关联。  
  
     **/Password** 选项仅与 **/User** 选项一起使用。 如果使用 **/Password** 选项，则使用提供的用户名和密码信息访问包。 如果省略 **/Password** 选项，则使用空密码。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
     如果省略 `/Server` 选项，则假定使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认本地实例。  
  
     `/SQL` 选项不能与 `/DTS` 或 `/File` 选项一起使用。 如果指定多个选项，`dtexec` 将失败。  
  
-   **/Su [m]**:可选。 显示一个递增计数器，其中包含下一个组件将接收的行数。  
  
-   **/U [ser]** _user_name_:  
                  可选。 允许检索受 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证保护的包。 仅当指定了 `/SQL` 选项时才使用此选项。 *user_name* 值可以用引号引起来。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va [lidate]**:  
                  可选。 在验证阶段之后停止执行包，而不实际运行包。 在验证期间使用的 **/WarnAsError**选项使`dtexec`将警告视为错误，因此如果在验证过程中出现警告时，包失败。  
  
-   **/Verifyb [uild]** _主要_[*; minor*[*; 生成*]]:可选。 根据验证阶段在 *major*、 *minor*和 *build* 参数中指定的内部版本号，验证包的内部版本号。 如果出现不匹配，则将不执行包。  
  
     这些值是长整数。 此参数可以使用以下三种格式之一，其中必须要有 *major* 的值：  
  
    -   *major*  
  
    -   *major*;*minor*  
  
    -   *major*; *minor*; *build*  
  
-   **/Verifyp [ackageID]** _packageID_:  
                  可选。 通过将要执行的包的 GUID 与 *package_id* 参数中指定的值进行比较，来验证该 GUID。  
  
-   **/Verifys [igned]**:  
                  可选。 导致 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 检查包的数字签名。 如果包未签名或签名无效，则包将失败。 有关详细信息，请参阅[使用数字签名标识包的源](../security/identify-the-source-of-packages-with-digital-signatures.md)。  
  
    > [!IMPORTANT]  
    >  在配置为检查包签名时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 仅检查数字签名是否存在、是否有效以及是否来自可信来源。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不检查包是否已更改。  
  
    > [!NOTE]  
    >  可选**BlockedSignatureStates**注册表值可指定比在中设置的数字签名选项限制性更强的设置[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]或在`dtexec`命令行。 在这种情况下，限制性更强的注册表设置将覆盖其他设置。  
  
-   **/Verifyv [ersionID]** _versionID_:可选。 通过将要执行的包的版本 GUID 与包验证阶段 *version_id* 参数中指定的值进行比较，来验证该 GUID。  
  
-   **/Vlog** _[Filespec]_:可选。 将所有 Integration Services 包事件写入设计包时已启用的日志提供程序。 若要让 Integration Services 启用文本文件的日志提供程序并将日志事件写入指定的文本文件，请将路径和文件名包括为 *Filespec* 参数。  
  
     如果不包括 *Filespec* 参数，Integration Services 将不会为文本文件启用日志提供程序。 Integration Services 仅将日志事件写入设计包时已启用的日志提供程序。  
  
-   **/W [arnAsError]**:  
                  可选。 导致包将警告视为错误，使得包在验证期间出现警告时失败。 如果验证期间无警告并且未指定 **/Validate** 选项，则执行包。  
  
-   **/X86**:可选。 使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在 64 位计算机上以 32 位模式运行包。 满足下列条件时此选项由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理设置：  
  
    -   作业步骤类型为 **“SQL Server Integration Services 包”**。  
  
    -   **“新建作业步骤”** 对话框中 **“执行选项”** 选项卡上的 **“使用 32 位运行时”** 选项处于选中状态。  
  
     您也可通过使用存储过程或 SQL Server 管理对象 (SMO) 以编程方式创建此作业，从而为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤设置此选项。  
  
     此选项仅由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理使用。 如果在命令提示符下运行 `dtexec` 实用工具则会忽略此选项。  
  
##  <a name="remark"></a> 注释  
 命令选项的指定顺序可以影响包的执行方式：  
  
-   选项的处理顺序与其在命令行中出现的顺序一致。 命令文件的读取顺序与其在命令行中出现的顺序一致。 命令文件中的命令的处理顺序也与其出现的顺序一致。  
  
-   如果在同一个命令行语句中多次出现相同的选项、参数或变量，则优先执行该选项的最后一个实例。  
  
-   **/Set** 和 **/ConfigFile** 选项将按其出现的顺序进行处理。  
  
##  <a name="example"></a> 示例  
 下面的示例演示如何使用`dtexec`命令提示实用工具来配置和执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包。  
  
 **“正在运行的包”**  
  
 若要使用 Windows 身份验证执行保存到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包，可使用以下代码：  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 若要执行保存到 SSIS 包存储区的“文件系统”文件夹中的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包，请使用以下代码：  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 若要验证使用 Windows 身份验证并保存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的包但不执行该包，可使用以下代码：  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 若要执行保存在文件系统中的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包，可使用以下代码：  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 若要执行保存在文件系统中的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包并指定日志选项，可使用以下代码：  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 若要执行使用 Windows 身份验证并保存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的默认本地实例的包，并在执行前查看其版本，可使用以下代码：  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 若要执行保存在文件系统中并在外部配置的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包，可使用以下代码：  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> [!NOTE]  
>  如果路径或文件名包含空格，则 /SQL、/DTS 或 /FILE 选项的 *package_path* 或 *filespec* 参数必须用引号引起来。 如果没有使用引号将参数引起来，则该参数不能包含空格。  
  
 **日志记录选项**  
  
 如果有三种日志项类型 A、B 和 C，以下不带参数的 **ConsoleLog** 选项可以显示所有三种日志类型和所有字段：  
  
```  
/CONSOLELOG  
```  
  
 以下选项显示所有日志类型，但只显示 Name 和 Message 列：  
  
```  
/CONSOLELOG NM  
```  
  
 以下选项仅显示日志项类型 A 的所有列：  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 以下选项仅显示日志项类型 A 的 Name 和 Message 列：  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 以下选项显示日志项类型 A 和 B 的日志项：  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 可以使用多个 **ConsoleLog** 选项来获得相同的结果：  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 如果使用不带参数的 **ConsoleLog** 选项，将显示所有字段。 包含 *list_options* 参数会导致以下示例仅显示日志项类型 A 和所有字段：  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 以下示例可以显示除日志项类型 A 以外的所有日志项，即显示日志项类型 B 和 C：  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 以下示例使用了多个 **ConsoleLog** 选项和一个排除条件，但获得的结果是相同的：  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 以下示例不显示日志消息，因为一个日志文件类型同时出现在包含列表和排除列表中时，该类型将被排除。  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **SET 选项**  
  
 以下示例显示如何使用 **/SET** 选项。从命令行启动包时，使用该选项可以更改任何包属性或变量的值。  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **项目选项**  
  
 以下示例显示如何使用 `/Project` 和 `/Package` 选项。  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 以下示例显示如何使用 `/Project` 和 `/Package` 选项并设置包参数和项目参数。  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **ISServer 选项**  
  
 以下示例显示如何使用 `/ISServer` 选项。  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 以下示例显示如何使用 `/ISServer` 选项并设置项目参数和连接管理器参数。  
  
```  
/Server localhost /ISServer "\SSISDB\MyFolder\Integration Services Project1\Package.dtsx" /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-tasks"></a>Related Tasks  
 [在 SQL Server Data Tools 中运行包](../run-a-package-in-sql-server-data-tools.md)  
  
## <a name="related-content"></a>相关内容  
 www.mattmasson.com 上的博客文章 [退出代码、DTEXEC 和 SSIS 目录](https://go.microsoft.com/fwlink/?LinkId=251523)。  
  
  
