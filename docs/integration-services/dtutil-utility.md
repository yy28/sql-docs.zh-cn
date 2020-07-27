---
title: dtutil 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- verifying packages
- checking packages
- moving packages
- packages [Integration Services], command line options
- command prompt [Integration Services]
- SQL Server Integration Services packages, command line options
- copying packages
- existence testing [Integration Services]
- Integration Services packages, command line options
- SSIS packages, command line options
- deleting packages
- dtutil utility
- removing packages
- relocating packages
ms.assetid: 6c7975ff-acec-4e6e-82e5-a641e3a98afe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d200856e098317f3158c2ace61c8e7cbb0001e88
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917103"
---
# <a name="dtutil-utility"></a>Encrypt

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  dtutil 命令提示实用工具用于管理   包[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。 该实用工具可以复制、移动、删除包，也可以验证包是否存在。 可对存储于以下三个位置之一的任何 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包执行上述操作：[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库、[!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区和文件系统。 如果此实用工具要访问存储在 **msdb**中的包，命令提示符可能要求输入用户名和密码。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，则命令提示符要求输入用户名和密码。 如果缺少用户名， **dtutil** 将尝试使用 Windows 身份验证登录到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 包的存储类型由 **/SQL**、 **/FILE**和 **/DTS** 选项标识。  
  
 **dtutil** 命令提示实用工具不支持使用命令文件或重定向。  
  
 **dtutil** 命令提示实用工具包含下列功能：  
  
-   命令提示符中的注释，使命令提示符操作可自行记录且更易于理解。  
  
-   覆盖保护，用于复制或移动包时在覆盖现有的包之前提示确认。  
  
-   控制台帮助，用于提供有关 **dtutil**命令选项的信息。  
  
> [!NOTE]  
>  在您连接到 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 实例时，也可以直观地在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中执行由 dtutil 执行的许多操作。 有关详细信息，请参阅[包管理（SSIS 服务）](../integration-services/service/package-management-ssis-service.md)。  
  
 这些选项的键入顺序不分先后。 竖线字符 ("|") 是 **OR** 运算符，用于显示可能的值。 您必须使用一个由 **OR** 竖线分隔的选项。  
  
 所有选项必须以斜杠 (/) 或减号 (-) 开头。 但是，斜杠或减号与选项的文本之间不能包含空格；否则，该命令将失败。  
  
 参数必须是用引号括起来的字符串，或是没有包含任何空格的字符串。  
  
 用引号引起来的字符串中的双引号表示转义的单引号。  
  
 除密码外，其他选项和参数都不区分大小写。  
  
 **64 位计算机上的安装注意事项**  
  
 在 64 位计算机上， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 将安装 64 位版本的 **dtexec** 实用工具 (dtexec.exe) 和 **dtutil** 实用工具 (dtutil.exe)。 若要安装这些 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 工具的 32 位版本，必须在安装过程中选择“客户端工具”或 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 。  
  
 默认情况下，同时安装了 64 位和 32 位版本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 命令提示实用工具的 64 位计算机将在命令提示符处运行 32 位版本。 运行 32 位版本的原因是：在 PATH 环境变量中，32 位版本的目录路径显示在 64 位版本的目录路径之前。 （通常，32 位目录路径是 \<drive>:\Program Files(x86)\Microsoft SQL Server\130\DTS\Binn，而 64 位目录路径是 \<drive>:\Program Files\Microsoft SQL Server\130\DTS\Binn。 ）  
  
> [!NOTE]  
>  如果使用 SQL Server 代理来运行此实用工具，则 SQL Server 代理会自动使用 64 位版本的实用工具。 SQL Server 代理使用注册表（而非 PATH 环境变量）来找到此实用工具的正确可执行文件。  
  
 若要确保在命令提示符处运行 64 位版本的实用工具，可以执行以下操作之一：  
  
-   打开“命令提示符”窗口，更改到包含 64 位版本的实用工具的目录 (\<drive>:\Program Files\Microsoft SQL Server\130\DTS\Binn)，然后从该位置运行此实用工具。  
  
-   在命令提示符处，输入 64 位版本的实用工具的完整路径 (\<drive>:\Program Files\Microsoft SQL Server\130\DTS\Binn) 来运行此实用工具。  
  
-   将 64 位路径 (\<drive>:\Program Files\Microsoft SQL Server\130\DTS\Binn) 置于 32 位路径(\<drive>:\Program Files(x86)\Microsoft SQL Server\130\DTS\Binn) 之前，可永久更改 PATH 环境变量中路径的顺序 。  
  
## <a name="syntax"></a>语法  
  
```dos
dtutil /option [value] [/option [value]]...  
```  
  
#### <a name="parameters"></a>parameters  
  
|选项|说明|  
|------------|-----------------|  
|/?|显示命令提示符选项。|  
|/C[opy] location;destinationPathandPackageName|指定对 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包的复制操作。 使用此参数需要先使用 **/FI**、 **/SQ**或 **/DT** 选项指定包的位置。 然后指定目标位置和目标包名称。 destinationPathandPackageName  参数指定 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包的复制目标。 如果目标 *location* 为 **SQL**，那么还必须在命令中指定 *DestUser*、 *DestPassword* 和 *DestServer* 参数。<br /><br /> 如果 **Copy** 操作的目标处已经有一个包， **dtutil** 将提示用户确认是否删除该包。 回答 **Y** 将覆盖包，回答 **N** 将结束程序。 如果该命令包含 *Quiet* 参数，则将不显示任何提示，并覆盖任何现有包。|  
|/Dec[rypt] password|（可选）。 设置加载使用密码加密的包时所用的解密密码。|  
|/Del[ete]|删除由 *SQL*、 *DTS* 或 *FILE* 选项指定的包。 如果 **dtutil** 无法删除包，则程序将结束。|  
|/DestP[assword] password|指定与 SQL 选项一起使用的密码，用于连接到使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 目标实例。 如果在不包含 *DESTPASSWORD* 选项的命令行中指定 *DTSUSER* ，则将生成错误。<br /><br /> 请注意： [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]。|  
|/DestS[erver] server_instance|指定与任何导致目标被保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的操作一起使用的服务器名称。 该选项用于在保存 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包时，标识一个非本地或非默认的服务器。 在不包含与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 关联的操作的命令行中指定 DESTSERVER 是错误的。 *SIGN SQL*、 *COPY SQL*或 *MOVE SQL* 选项的相应命令都可与该选项结合使用。<br /><br /> 通过在服务器名中添加反斜杠和实例名称，可以指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例名称。|  
|/DestU[ser] username|指定与 SIGN SQL、COPY SQL 和 MOVE SQL 选项一起使用的用户名，以连接到使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例。 在不包含 *DESTUSER* 、 *SIGN SQL*或 *COPY SQL*选项的命令行中指定 *MOVE SQL* 是错误的。|  
|/Dump *process ID*|（可选）使指定进程（ **dtexec** 实用工具或 **dtsDebugHost.exe** 进程）暂停，并创建调试转储文件 .mdmp 和 .tmp。<br /><br /> 请注意：若要使用 **/Dump**选项，则必须具有“调试程序”用户权限 (SeDebugPrivilege)。<br /><br /> 若要查找要暂停的进程的 *process ID* ，请使用 Windows 任务管理器。<br /><br /> 默认情况下，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 将调试转储文件存储在 \<drive>:\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps 文件夹中。<br /><br /> 有关 **dtexec** 实用工具和 **dtsDebugHost.exe** 进程的详细信息，请参阅 [dtexec Utility](../integration-services/packages/dtexec-utility.md) 和 [Building, Deploying, and Debugging Custom Objects](../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。<br /><br /> 有关调试转储文件的详细信息，请参阅 [Generating Dump Files for Package Execution](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)。<br /><br /> 请注意：调试转储文件可能包含敏感信息。 使用访问控制列表 (ACL) 来限制对这些文件的访问，或将文件复制到具有受限访问权限的文件夹中。|  
|/DT[S] filespec|指定要对其执行操作的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包位于 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区中。 filespec  参数必须包括以 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区的根开头的文件夹路径。 默认情况下，该配置文件中的根文件夹的名称为“MSDB”和“File System”。 必须使用双引号分隔包含空间的路径。<br /><br /> 如果指定 DT[S] 选项的命令行中还有以下任一选项，则返回 DTEXEC_DTEXECERROR：<br /><br /> **FILE**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/En[crypt] {SQL &#124; FILE}; Path;ProtectionLevel[;password]|（可选）。 使用指定的保护级别和密码对加载的包进行加密，并将其保存到 *Path*中指定的位置。 *ProtectionLevel* 确定是否需要密码。<br /><br /> SQL  - Path 为目标包名称。<br /><br /> FILE  - Path 为包的完全限定路径和文件名。<br /><br /> DTS  - 当前不支持该选项。<br /><br /> *ProtectionLevel* 选项：<br /><br /> 级别 0：提取敏感信息。<br /><br /> 级别 1：使用本地用户凭据对敏感信息进行加密。<br /><br /> 级别 2：使用必需的密码对敏感信息进行加密。<br /><br /> 级别 3：使用必需的密码对包进行加密。<br /><br /> 级别 4：使用本地用户凭据对包进行加密。<br /><br /> 级别 5：包使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 存储加密。|  
|/Ex[ists]|（可选）。 用于确定包是否存在。 **dtutil** 尝试查找用 *SQL*、 *DTS* 或 *FILE* 选项指定的包。 如果 **dtutil** 找不到指定的包，则返回 DTEXEC_DTEXECERROR。|  
|/FC[reate] {SQL  &#124; DTS  };ParentFolderPath;NewFolderName|（可选）。 创建一个新文件夹，该文件夹的名称是在 *NewFolderName*中指定的。 新文件夹的位置由 *ParentFolderPath*指示。|  
|/FDe[lete] {SQL  &#124; DTS  }[;ParentFolderPath;FolderName]|（可选）。 从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 中删除由 FolderName  中的名称指定的文件夹。 要删除的文件夹的位置由 *ParentFolderPath*指示。|  
|/FDi[rectory] {SQL  &#124; DTS  };FolderPath[;S]|（可选）。 列出 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的文件夹中的内容（文件夹和包）。 可选参数 *FolderPath* 指定要查看其内容的文件夹。 可选参数 *S* 指定要查看 *FolderPath*中所指定文件夹的子文件夹的内容列表。|  
|/FE[xists ] {SQL  &#124; DTS  };FolderPath|（可选）。 验证 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中是否存在指定的文件夹。 *FolderPath* 参数是要验证的文件夹的路径和名称。|  
|/Fi[le] filespec|此选项指定要操作的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包位于文件系统中。 filespec  值可以是通用命名约定 (UNC) 路径或本地路径。<br /><br /> 如果指定 File  选项的命令行中还有以下任一选项，则返回 DTEXEC_DTEXECERROR：<br /><br /> **DTS**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/FR[ename] {SQL  &#124; DTS  } [;ParentFolderPath; OldFolderName;NewFolderName]|（可选）。 重命名 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的文件夹。 *ParentFolderPath* 是要重命名的文件夹的位置。 *OldFolderName* 是文件夹的当前名称， *NewFolderName* 是要为文件夹提供的新名称。|  
|/H[elp] option|显示详细的文本帮助，该帮助可以显示 **dtutil** 的各个选项并说明其用法。 该选项参数是可选的。 如果包含该参数，则帮助文本将包含有关指定选项的详细信息。 以下示例将显示所有选项的帮助：<br /><br /> `dtutil /H`<br /><br /> 下列两个示例显示如何使用 /H  选项显示特定选项（本例中为 /Q [uiet]  选项）的详细帮助：<br /><br /> `dtutil /Help Quiet`<br /><br /> `dtutil /H Q`|  
|/I[DRegenerate]|为包创建新的 GUID 并更新包 ID 属性。 复制包后，包 ID 保持不变；因此，对于两个包，日志文件包含的 GUID 相同。 该操作为新复制的包创建新的 GUID，以便将其与原始包区分开。|  
|/M[ove] {SQL  &#124; File  &#124; DTS  }; pathandname|指定对 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包的移动操作。 若要使用该参数，请先使用 **/FI**、 **/SQ**或 **/DT** 选项指定包的位置。 然后指定 **Move** 操作。 此操作需要两个由分号分隔的参数：<br /><br /> 目标参数可指定 *SQL*、 *FILE*或 *DTS*。 *SQL* 目标可包含 *DESTUSER*、 *DESTPASSWORD*和 *DESTSERVER* 选项。<br /><br /> pathandname  参数指定包位置：SQL  使用包路径和包名称，FILE  使用 UNC 或本地路径，DTS  使用相对于 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区的根目录的位置。 如果目标为 *FILE* 或 *DTS*，则路径参数将不包含文件名， 而使用指定位置的包名称作为文件名。<br /><br /> <br /><br /> 如果 **MOVE** 操作的目标处已经有一个包，则 **dtutil** 将提示你确认是否要覆盖这个包。 回答 **Y** 将覆盖包，回答 **N** 将结束程序。 如果该命令包含 *QUIET* 选项，则将不显示任何提示，并覆盖任何现有包。|  
|/Q[uiet]|在执行包含 **COPY**、 **MOVE**或 **SIGN** 选项的命令时，停止可能显示的确认提示。 如果目标计算机中已经存在与指定包同名的包，或者如果已经对指定包进行了签名，则将显示这些提示。|  
|/R[emark] text|向命令行中添加注释。 该注释参数是可选的。 如果注释文本包含空格，则文本必须用引号引起来。 可以在一个命令行中包含多个 REM 选项。|  
|/Si[gn] {SQL  &#124; File  &#124; DTS  }; path  ; hash|对 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包进行签名。 此操作使用三个由分号分隔的必要参数；destination、path 和 hash：<br /><br /> 目标参数可指定 *SQL*、 *FILE*或 *DTS*。 SQL 目标可包含 *DESTUSER*、 *DESTPASSWORD* 和 *DESTSERVER* 选项。<br /><br /> Path 参数指定要操作的包的位置。<br /><br /> Hash 参数指定以长度可变的十六进制字符串表示的证书标识符。<br /><br /> 有关详细信息，请参阅 [使用数字签名标识包的源](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)。<br /><br /> <br /><br /> **\*\* 重要提示 \*\*** 在配置为检查包签名时， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 仅检查数字签名是否存在、是否有效以及是否来自可信来源。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]*不* 检查包是否已更改。|  
|/SourceP[assword] password|指定与 *SQL* 和 *SOURCEUSER* 选项一起使用的密码，以便可以对存储在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 实例（使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 目标实例。 在不包含 *SOURCEUSER* 选项的命令行中指定 **SOURCEPASSWORD** 是错误的。<br /><br /> 请注意：[!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SourceS[erver] server_instance|指定与 **SQL** 选项一起使用的服务器名称，以便可以检索存储在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 在不包含 SIGN SQL、COPY、SQL 或 MOVE SQL 选项的命令行中指定 SOURCESERVER 是错误的       。<br /><br /> 通过在服务器名中添加反斜杠和实例名称，可以指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例名称。|  
|/SourceU[ser] username|指定与 *SOURCESERVER* 选项一起使用的服务器名称，以便可以检索存储在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 身份验证的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 目标实例。 在不包含 *SOURCEUSER* 、 *SIGN SQL*或 *COPY SQL*选项的命令行中指定 *MOVE SQL* 是错误的。<br /><br /> 请注意：[!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SQ[L] package_path|指定 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包的位置。 该选项指示包存储在 **msdb** 数据库中。 package_path  参数指定 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包的路径和名称。 文件夹名以反斜杠结尾。<br /><br /> 如果指定 SQL  选项的命令行中还有以下任一选项，则返回 DTEXEC_DTEXECERROR：<br /><br /> *DTS*<br /><br /> *FILE*<br /><br /> *SQL* 选项可以不附带实例，也可以附带下列选项的某个实例：<br /><br /> *SOURCEUSER*<br /><br /> *SOURCEPASSWORD*<br /><br /> *SOURCESERVER*<br /><br /> <br /><br /> 如果不包含 *SOURCEUSERNAME* ，则使用 Windows 身份验证来访问包。 仅当存在*SOURCEPASSWORD* 时，才允许指定 *SOURCEUSER* 。 如果不包含 *SOURCEPASSWORD* ，则使用空密码。<br /><br /> **\*\* 重要说明 \*\*** [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]|  
  
## <a name="dtutil-exit-codes"></a>dtutil 退出代码  
 如果检测到语法错误、使用了错误参数或指定了无效的选项组合，**dtutil** 将设置退出代码以向你发出警报。 否则，该实用工具将报告“操作已成功完成”。下表列出了 **dtutil** 实用工具在退出时可以设置的值。  
  
|值|说明|  
|-----------|-----------------|  
|0|已成功执行此实用工具。|  
|1|此实用工具已失败。|  
|4|此实用工具找不到请求的包。|  
|5|此实用工具无法加载请求的包。|  
|6|此实用工具无法解析命令行，因为它包含语法或语义错误。|  
  
## <a name="remarks"></a>备注  
 命令文件或重定向不能与 **dtutil**一起使用。  
  
 命令行中选项的顺序不分先后。  
  
## <a name="examples"></a>示例  
 以下示例详细说明了典型的命令行使用方法。  
  
### <a name="copy-examples"></a>复制示例  
 若要将存储在使用 Windows 身份验证的 **本地实例中** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的包复制到 SSIS 包存储区，可使用以下语法：  
  
```dos
dtutil /SQL srcPackage /COPY DTS;destFolder\destPackage   
```  
  
 若要将包从文件系统中的某个位置复制到其他位置，并为副本提供一个不同的名称，可使用以下语法：  
  
```dos
dtutil /FILE c:\myPackages\mypackage.dtsx /COPY FILE;c:\myTestPackages\mynewpackage.dtsx  
```  
  
 若要将本地文件系统中的包复制到其他计算机上承载的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，可使用以下语法：  
  
```dos
dtutil /FILE c:\sourcepkg.dtsx /DestServer <servername> /COPY SQL;destpkgname  
```  
  
 由于未使用 /DestU[ser]  和 /DestP[assword]  选项，因此假定使用 Windows 身份验证。  
  
 若要在复制某个包后为其创建新的 ID，可使用以下语法：  
  
```dos
dtutil /I /FILE copiedpkg.dtsx   
```  
  
 若要为某特定文件夹中的所有包创建新的 ID，可使用以下语法：  
  
```dos
for %%f in (C:\test\SSISPackages\*.dtsx) do dtutil.exe /I /FILE %%f  
```  
  
 在命令提示符下键入命令时，使用一个百分号 (%)。 如果在批处理文件内使用命令，则使用两个百分号 (%%)。  
  
### <a name="delete-examples"></a>删除示例  
 若要删除存储在使用 Windows 身份验证的 **实例中** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的包，可使用以下语法：  
  
```dos
dtutil /SQL delPackage /DELETE  
```  
  
 若要删除存储在使用 **身份验证的** 实例中 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的包，可使用以下语法：  
  
```dos
dtutil /SQL delPackage /SOURCEUSER srcUserName /SOURCEPASSWORD #8nGs*w7F /DELETE  
```  
  
> [!NOTE]  
>  若要从命名服务器中删除包，可包含 **SOURCESERVER** 选项及其参数。 使用该 *SQL* 选项只能指定服务器。  
  
 若要删除存储于 SSIS 包存储区中的包，可使用以下语法：  
  
```dos
dtutil /DTS delPackage.dtsx /DELETE  
```  
  
 若要删除存储在文件系统中的包，可使用以下语法：  
  
```dos
dtutil /FILE c:\delPackage.dtsx /DELETE  
```  
  
### <a name="exists-examples"></a>存在示例  
 若要确定使用 Windows 身份验证的 **本地实例中的** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中是否存在包，可使用以下语法：  
  
```dos
dtutil /SQL srcPackage /EXISTS  
```  
  
 若要确定使用 **身份验证的** 本地实例中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中是否存在包，可使用以下语法：  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD *hY$d56b /EXISTS  
```  
  
> [!NOTE]  
>  若要确定命名服务器上是否存在包，可包含 **SOURCESERVER** 选项及其参数。 使用该 SQL 选项只能指定服务器。  
  
 若要确定本地包存储区中是否存在包，可使用以下语法：  
  
```dos
dtutil /DTS srcPackage.dtsx /EXISTS  
```  
  
 若要确定本地文件系统中是否存在包，可使用以下语法：  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /EXISTS  
```  
  
### <a name="move-examples"></a>移动示例  
 若要将 SSIS 包存储区中存储的包移到使用 Windows 身份验证的 **本地实例中的** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库，可使用以下语法：  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE SQL;destPackage  
```  
  
 若要将使用 **身份验证的** 本地实例中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中存储的包移到使用 **身份验证的** 的另一本地实例中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库，可使用以下语法：  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD $Hj45jhd@X /MOVE SQL;destPackage /DESTUSER destUserName /DESTPASSWORD !38dsFH@v  
```  
  
> [!NOTE]  
>  若要将一个命名服务器中的包移动到另一个命名服务器，可包含 **SOURCES** 和 **DESTS** 选项及其参数。 只能使用 *SQL* 选项指定服务器。  
  
 若要移动存储在 SSIS 包存储区中的包，可使用以下语法：  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE DTS;destPackage.dtsx  
```  
  
 若要移动存储在文件系统中的包，可使用以下语法：  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /MOVE FILE;c:\destPackage.dtsx  
```  
  
### <a name="sign-examples"></a>签名示例  
 若要对存储在使用 Windows 身份验证的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 本地实例中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的包签名，可使用以下语法：  
  
```dos
dtutil /FILE srcPackage.dtsx /SIGN FILE;destpkg.dtsx;1767832648918a9d989fdac9819873a91f919  
```  
  
 若要查找有关证书的信息，请使用 **CertMgr**。 在 **CertMgr** 实用工具中选择证书可查看哈希代码，然后单击“查看”  可查看属性。 **“详细信息”** 选项卡提供了有关证书的详细信息。 **Thumbprint** 属性在删除空格后被用作哈希值。  
  
> [!NOTE]  
>  此示例中用到的哈希并不是真正的哈希。  
  
 有关详细信息，请参阅 [使用 Authenticode 签名和检查代码](https://go.microsoft.com/fwlink/?LinkId=78100)中的 CertMgr 部分。  
  
### <a name="encrypt-examples"></a>加密示例  
 以下示例使用完全包加密和密码将基于文件的 PackageToEncrypt.dtsx 加密为基于文件的 EncryptedPackage.dts。 加密所用的密码是 *EncPswd*。  
  
```dos
dtutil /FILE PackageToEncrypt.dtsx /ENCRYPT file;EncryptedPackage.dtsx;3;EncPswd  
```  
  
## <a name="see-also"></a>另请参阅  
[运行 Integration Services (SSIS) 包](../integration-services/packages/run-integration-services-ssis-packages.md)  
  
  
