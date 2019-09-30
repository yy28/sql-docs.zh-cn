---
title: 包管理（SSIS 服务）| Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dtsserver.importpackage.f1
- sql13.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 33ce0a748381e425371b6f36c1ceeaaba4b62501
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296881"
---
# <a name="package-management-ssis-service"></a>包管理（SSIS 服务）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  包管理包括监视、管理、导入和导出包。  
 
 ## <a name="package-store"></a>包存储区  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供两个用于访问包的顶层文件夹： 
 - **“正在运行的包”** 
 - **“已存储的包”**

 **“正在运行的包”** 文件夹列出当前正在服务器上运行的包。 **“已存储的包”** 文件夹列出包存储区中保存的包。 这些只是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务所管理的包。 包存储区可以同时包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置文件中列出的 msdb 数据库和文件系统文件夹或只包含其中的一项。 配置文件指定要管理的 msdb 数据库和文件系统文件夹。 您也可以将包存储在文件系统中不受 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务管理的其他位置。  
  
 保存到 msdb 的包存储在名为 sysssispackages 的表中。 将包保存到 msdb 时，可以按逻辑文件夹对包分组。 使用逻辑文件夹有助于按用途整理包，或者筛选 sysssispackages 表中的包。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中创建新的逻辑文件夹。 默认情况下，任何添加到 msdb 的逻辑文件夹将自动包括在包存储区中。  
  
 所创建的逻辑文件夹表示为 msdb 中 sysssispackagefolders 表的行。 sysssispackagefolders 中的 folderid 列和 parentfolderid 列定义文件夹层次结构。 msdb 中的根逻辑文件夹是 sysssispackagefolders 中 parentfolderid 列为 null 值的行。 有关详细信息，请参阅 [sysssispackages (Transact-SQL)](../../relational-databases/system-tables/sysssispackages-transact-sql.md) 和 [sysssispackagefolders (Transact-SQL)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)。  
  
 在打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]时，你将看到在“已存储的包”文件夹中列出的由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务管理的 msdb 文件夹。 如果配置文件指定根文件系统文件夹，则“已存储的包”文件夹还会列出保存到文件系统的这些文件夹和所有子文件夹中的包。  
  
 您可以将包存储在任何文件系统文件夹中，但是除非将该文件夹添加到包存储区配置文件中的文件夹列表，否则这些包不会在 **“已存储的包”** 文件夹的子文件夹中列出。 有关配置文件的详细信息，请参阅 [Integration Services 服务（SSIS 服务）](../../integration-services/service/integration-services-service-ssis-service.md)的早期版本向后兼容。  
  
 **“正在运行的包”** 文件夹不包含子文件夹，也不可扩展。  
  
 默认情况下，“已存储的包”  文件夹包含两个文件夹：“文件系统”  和 MSDB  。 **“文件系统”** 文件夹列出保存到文件系统中的包。 这些文件的位置在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置文件中指定。 默认文件夹是 Packages 文件夹，它位于 %Program Files%\Microsoft SQL Server\100\DTS 下。 **MSDB** 文件夹列出已经保存到服务器上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] msdb 数据库中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包。 sysssispackages 表包含保存到 msdb 中的包。  
  
 若要查看包存储区中的包列表，必须打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
## <a name="monitor-running-packages"></a>监视正在运行的包  
 “正在运行的包”  文件夹列出当前正在运行的包。 若要在 **的** “摘要” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]页上查看当前包的信息，请单击 **“正在运行的包”** 文件夹。 **“摘要”** 页上列有正在运行的包的执行持续时间等信息。 您可以选择刷新该文件夹，以显示最新的信息。  
  
 若要查看 **“摘要”** 页上某个正在运行的包的信息，请单击此包。 **“摘要”** 页显示包的版本和说明等信息。  
  
右键单击“正在运行的包”  文件夹中某个正在运行的包，然后单击“停止”  ，可以使该包停止运行。  
  
## <a name="view-packages-in-ssms"></a>在 SSMS 中查看包
    
 本过程介绍在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中如何连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并查看 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务所管理的包的列表。  
  
### <a name="to-connect-to-integration-services"></a>连接到 Integration Services  
  
1.  单击 **“开始”** ，依次指向 **“所有程序”** 和 **Microsoft SQL Server**，然后单击 **SQL Server Management Studio**。  
  
2.  在 **“连接到服务器”** 对话框中，在 **“服务器类型”** 列表中选择 **Integration Services** ，在 **“服务器名称”** 框中提供服务器名称，然后单击 **“连接”** 。  
  
    > [!IMPORTANT]  
    >  如果无法连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，则 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务可能未运行。 若要了解该服务的状态，请单击 **“开始”** ，依次指向 **“所有程序”** 、 **Microsoft SQL Server**和 **“配置工具”** ，再单击 **“SQL Server 配置管理器”** 。 在左窗格中，单击 **“SQL Server 服务”** 。 在右窗格中，查找 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。 如果该服务尚未运行，请启动该服务。  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 默认情况下，会打开对象资源管理器窗口并定位在 SQL Server Management Studio 左下角。 如果对象资源管理器未打开，请单击 **“视图”** 菜单上的 **“对象资源管理器”** 。  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>查看 Integration Services 服务管理的包  
  
1.  在对象资源管理器中，展开“已存储的包”文件夹。  
  
2.  展开“已存储的包”子文件夹，以显示包。  

## <a name="import-and-export-packages"></a>导入和导出包
 
 包既可以保存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 数据库的 sysssispackages 表中，也可以保存在文件系统中。  
  
 包存储区是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务监视和管理的逻辑存储区，它包括在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置文件中指定的 msdb 数据库和文件系统。  
  
 您可以在下列存储类型之间导入和导出包：  
  
-   文件系统中任意位置的文件系统文件夹。  
  
-   SSIS 包存储区中的文件夹。 这两个默认文件夹分别称为“文件系统”和“MSDB”。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 数据库。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了导入和导出包的功能，通过此功能可以更改包的存储格式和位置。 使用导入和导出功能，您可以将包添加到文件系统、包存储区或 msdb 数据库，然后将包从一种存储格式复制为另一种存储格式。 例如，保存在 msdb 中的包可以复制到文件系统中，反之亦然。  
  
 还可以使用 **dtutil** 命令提示实用工具 (dtutil.exe) 将包复制为其他格式。 有关详细信息，请参阅 [dtutil Utility](../../integration-services/dtutil-utility.md)。  
  
 您可以从以下位置导出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，或将包导入以下位置：  
  
-   可以导入存储在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例、文件系统或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区中的包。 导入的包将保存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区中的文件夹。  
  
-   可以将存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例、文件系统或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区中的包导出至不同的存储格式和位置。  
  
 但对于在不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之间导入和导出包，存在一些限制：  
  
-   对于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]实例，可以从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]实例导入包，但不能将包导出到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]实例。  
  
-   对于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]实例，不能从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]实例导入包，也不能将包导出到该实例。  
  
 下列过程说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 导入或导出包。  
  
### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 导入包  
  
1.  单击  “开始”，指向 **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后单击 **SQL Server Management Studio**。  
  
2.  在 **“连接到服务器”** 对话框中，设置以下选项：  
  
    -   在 **“服务器类型”** 框中，选择 **“Integration Services”** 。  
  
    -   在“服务器名称”框中，提供服务器名称，或者单击“\<浏览更多...>”，并找到要使用的服务器   。  
  
3.  如果对象资源管理器未打开，请在 **“视图”** 菜单上，单击 **“对象资源管理器”** 。  
  
4.  在对象资源管理器中，展开 **“已存储的包”** 文件夹。  
  
5.  展开子文件夹，找到要向其中导入包的文件夹。  
  
6.  右键单击该文件夹，单击“导入包”。  然后请执行下列操作之一：  
  
    -   若要从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例导入，请选择 **“SQL Server”** 选项，然后指定服务器并选择身份验证模式。 如果选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供用户名和密码。  
  
         单击浏览按钮 (…)，选择要导入的包，再单击“确定”   。  
  
    -   若要从文件系统导入，请选择 **“文件系统”** 选项。  
  
         单击浏览按钮 (…)，选择要导入的包，然后单击“打开”   。  
  
    -   若要从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区中导入，请选择 **“SSIS 包存储区”** 选项，并指定服务器。  
  
         单击浏览按钮 (…)，选择要导入的包，再单击“确定”   。  
  
7.  根据需要，也可以更新包名称。  
  
8.  若要更新包的保护级别，请单击浏览按钮 (…)，然后使用“包保护级别”对话框选择其他保护级别   。 如果选定了 **“使用密码加密敏感数据”** 或 **“使用密码加密所有数据”** 选项，请键入并确认密码。  
  
9. 单击 **“确定”** ，完成导入操作。  
  
### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 导出包  
  
1.  单击  “开始”，指向 **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后单击 **SQL Server Management Studio**。  
  
2.  在 **“连接到服务器”** 对话框中，设置下列选项：  
  
    -   在 **“服务器类型”** 框中，选择 **“Integration Services”** 。  
  
    -   在“服务器名称”框中，提供服务器名称，或者单击“\<浏览更多...>”，并找到要使用的服务器   。  
  
3.  如果对象资源管理器未打开，请在 **“视图”** 菜单上，单击 **“对象资源管理器”** 。  
  
4.  在对象资源管理器中，展开 **“已存储的包”** 文件夹。  
  
5.  展开子文件夹以找到要导出的包。  
  
6.  右键单击该包，单击“导出”  ，然后执行以下操作之一：  
  
    -   若要导出到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例，请选择 **SQL Server** 选项，然后指定服务器并选择身份验证模式。 如果选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供用户名和密码。  
  
         单击浏览按钮 (…)，展开“SSIS 包”文件夹以找到要存储此包的文件夹   。 也可以更新此包的默认名称，然后单击 **“确定”** 。  
  
    -   要导出到文件系统，请选择 **“文件系统”** 选项。  
  
         单击浏览按钮 (…) 以查找要向其中导出包的文件夹，键入包文件的名称，然后单击“保存”   。  
  
    -   若要导出到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区，请选择 **“SSIS 包存储区”** 选项并指定服务器。  
  
         单击浏览按钮 (…)，展开“SSIS 包”文件夹，然后选择要存储此包的文件夹   。 也可以在 **“包名称”** 文本框中为包键入新名称。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  若要更新包的保护级别，请单击浏览按钮 (…)，然后使用“包保护级别”对话框选择其他保护级别   。 如果选定了 **“使用密码加密敏感数据”** 或 **“使用密码加密所有数据”** 选项，请键入并确认密码。  
  
8.  单击 **“确定”** ，完成导出操作。  

## <a name="import-package-dialog-box-ui-reference"></a>“导入包”对话框 UI 参考
  可以使用 **中的** “导入包” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框，导入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包以及设置或修改包的保护级别。  
  
### <a name="options"></a>选项  
 **包位置**  
 选择要向其中导入包的存储位置的类型。 可用选项包括：  
  
 **SQL Server**  
  
 **文件系统**  
  
 **SSIS 包存储区**  
  
 **Server**  
 键入服务器名称或从列表中选择一个服务器。  
  
 **身份验证**  
 选择 Windows 身份验证或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 只有在存储位置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，此选项才可用。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。  
  
 **身份验证类型**  
 选择身份验证类型。  
  
 **User name**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供用户名。  
  
 **密码**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供密码。  
  
 **包路径**  
 键入包的路径，或单击浏览按钮 (…) 并查找包  。  
  
 **包名称**  
 可以根据需要对包进行重命名。 默认名称是要导入的包的名称。  
  
 **保护级别**  
 单击浏览按钮 (…)，然后在“包保护级别”对话框中更新保护级别   。 有关详细信息，请参阅 [“包和项目保护级别”对话框](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog)。  

## <a name="export-package-dialog-box-ui-reference"></a>“导出包”对话框 UI 参考
  可以使用 **中的** “导出包” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框，将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包导出到其他位置并根据需要修改包的保护级别。  
  
### <a name="options"></a>选项  
 **包位置**  
 选择要将包导出到的存储区的类型。 可用选项包括：  
  
 **SQL Server**  
  
 **“文件系统”**  
  
 **SSIS 包存储**  
  
 **Server**  
 键入服务器名称或从列表中选择一个服务器。  
  
 **身份验证**  
 选择 Windows 身份验证或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 只有在存储位置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，此选项才可用。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。  
  
 **身份验证类型**  
 选择身份验证类型。  
  
 **User name**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供用户名。  
  
 **密码**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供密码。  
  
 **包路径**  
 键入包路径，或单击浏览按钮 (…)，然后定位存储包的文件夹  。  
  
 **保护级别**  
 单击浏览按钮 (…)，然后在“包保护级别”对话框中更新保护级别   。 有关详细信息，请参阅 [“包和项目保护级别”对话框](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog)。  

## <a name="back-up-and-restore-packages"></a>备份和还原包
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包可以保存到文件系统或 msdb（一种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库）中。 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份和还原功能来备份和还原保存到 msdb 中的包。  
  
 有关备份和还原 msdb 数据库的详细信息，请单击下列某个主题：  
  
-   [SQL Server 数据库的备份和还原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [备份和还原系统数据库 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括可用于管理包的 **dtutil** 命令提示实用工具 (dtutil.exec)。 有关详细信息，请参阅 [dtutil Utility](../../integration-services/dtutil-utility.md)。  
  
### <a name="configuration-files"></a>配置文件  
 包所包括的所有配置文件都存储在文件系统中。 在备份 msdb 数据库时并不会备份这些文件；因此，你应该确保定期备份配置文件，以便保护保存到 msdb 中的包。 若要将配置包括在 msdb 数据库的备份中，应该考虑使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置类型，而不使用基于文件的配置。  
  
### <a name="packages-stored-in-the-file-system"></a>在文件系统中存储的包  
 备份服务器文件系统的计划中应当包括对保存到文件系统的包的备份。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置文件的默认名称为 MsDtsSrvr.ini.xml，它列出服务器上该服务所监视的文件夹。 您应该确保备份这些文件夹。 另外，包可以存储在服务器上的其他文件夹中，因此应该确保在备份中包括这些文件夹。  

## <a name="see-also"></a>另请参阅  
 [Integration Services 服务（SSIS 服务）](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  
