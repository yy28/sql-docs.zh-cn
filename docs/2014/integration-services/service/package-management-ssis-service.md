---
title: 包管理（SSIS 服务）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 89e925d72b4ca4815c05e9f4ab67211a1a7ea980
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62766620"
---
# <a name="package-management-ssis-service"></a>包管理（SSIS 服务）
  包的管理涉及的任务包括以下任务：  
  
-   监视正在运行的包  
  
-   管理包存储  
  
-   导入和导出包  
  
> [!IMPORTANT]  
>  本主题论述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]支持服务以便与的早期版本向后兼容[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
## <a name="package-store"></a>包存储区  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]提供了两个用于访问[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包的顶级文件夹： "**正在运行包**" 和 "已存储的**包**"。 
  **“正在运行的包”** 文件夹列出当前正在服务器上运行的包。 
  **“已存储的包”** 文件夹列出包存储区中保存的包。 这些只是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务所管理的包。 包存储区可以同时包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置文件中列出的 msdb 数据库和文件系统文件夹或只包含其中的一项。 配置文件指定要管理的 msdb 数据库和文件系统文件夹。 您也可以将包存储在文件系统中不受 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务管理的其他位置。  
  
 保存到 msdb 的包存储在名为 sysssispackages 的表中。 将包保存到 msdb 时，也可以按逻辑文件夹对包分组。 使用逻辑文件夹可以帮助你按目的组织包，或者筛选 sysssispackages 表中的包。 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]来创建新的逻辑文件夹。 默认情况下，任何添加到 msdb 的逻辑文件夹将自动包括在包存储区中。  
  
 在 msdb 中创建的用于对包进行分组的逻辑文件夹将表示为 msdb 中 sysssispackagefolders 表的行。 sysssispackagefolders 中的 folderid 列和 parentfolderid 列定义文件夹层次结构。 msdb 中的根逻辑文件夹是 sysssispackagefolders 中 parentfolderid 列为 null 值的行。 有关详细信息，请参阅 [sysssispackages (Transact SQL)](/sql/relational-databases/system-tables/sysssispackages-transact-sql) 和 [sysssispackagefolders (Transact SQL)](/sql/relational-databases/system-tables/sysssispackagefolders-transact-sql)。  
  
 在打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]时，你将看到在“已存储的包”文件夹中列出的由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务管理的 msdb 文件夹。 如果配置文件指定根文件系统文件夹，则“已存储的包”文件夹还会列出保存到文件系统的这些文件夹和所有子文件夹中的包。  
  
 您可以将包存储在任何文件系统文件夹中，但是除非将该文件夹添加到包存储区配置文件中的文件夹列表，否则这些包不会在 **“已存储的包”** 文件夹的子文件夹中列出。 有关配置文件的详细信息，请参阅[配置 Integration Services Service (SSIS 服务)](integration-services-service-ssis-service.md)。  
  
 
  **“正在运行的包”** 文件夹不包含子文件夹，也不可扩展。  
  
 默认情况下， **“已存储的包”** 文件夹包含两个文件夹： **“文件系统”** 和 **MSDB**。 
  **“文件系统”** 文件夹列出保存到文件系统中的包。 这些文件的位置在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置文件中指定。 默认文件夹是 Packages 文件夹，它位于 %Program Files%\Microsoft SQL Server\100\DTS 下。 
  **MSDB** 文件夹列出已经保存到服务器上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] msdb 数据库中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包。 sysssispackages 表包含保存到 msdb 中的包。  
  
 若要查看包存储区中的包列表，必须打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 有关详细信息，请参阅 [在 SQL Server Management Studio 中查看 Integration Services 包（SSIS 服务）](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)的早期版本向后兼容。  
  
## <a name="monitoring-running-packages"></a>监视正在运行的包  
 
  **“正在运行的包”** 文件夹列出当前正在运行的包。 若要在 **的** “摘要” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]页上查看当前包的信息，请单击 **“正在运行的包”** 文件夹。 
  **“摘要”** 页上列有正在运行的包的执行持续时间等信息。 您可以选择刷新该文件夹，以显示最新的信息。  
  
 若要查看 **“摘要”** 页上某个正在运行的包的信息，请单击此包。 
  **“摘要”** 页显示包的版本和说明等信息。  
  
 右键单击“正在运行的包”**** 文件夹中某个正在运行的包，然后单击“停止”****，可以使该包停止运行。  
  
## <a name="managing-package-storage"></a>管理包存储  
 若要组织包，可以向 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务在其配置文件中所列出的包存储区根文件夹内添加自定义文件夹。 默认情况下，根文件夹是 **“文件系统”** 和 **MSDB** 文件夹。 例如，您可能希望在 **“文件系统”** 文件夹中添加一个 **“数据清理”** 文件夹，该文件夹将包含用于清理数据的所有包。 可以将自定义文件夹添加到自定义文件夹中，从而创建适合您需要的嵌套式文件夹层次结构。 可以删除和重命名自定义文件夹，但是，不能删除或重命名配置文件所指定的根文件夹。 若要更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 列出的根文件夹，必须更新配置文件。  
  
 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](../configuring-the-integration-services-service-ssis-service.md)。  
  
## <a name="importing-and-exporting-packages"></a>导入和导出包  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包可以保存到 msdb 数据库或文件系统中。 使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的导入或导出功能，可以将包从一种存储类型复制到其他存储类型。 还可以将包导入相同的存储类型，然后将该包命名为不同的名称，从而创建包的副本。 
  **dtutil** 命令提示实用工具 (dtutil.exe) 也可以用于导入和导出包。  
  
 有关详细信息，请参阅 [dtutil Utility](../dtutil-utility.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [&#40;SSIS 服务导入和导出包&#41;](../import-and-export-packages-ssis-service.md)  
  
-   [查看 SQL Server Management Studio &#40;SSIS 服务中 Integration Services 包&#41;](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 服务（SSIS 服务）](integration-services-service-ssis-service.md)  
  
  
