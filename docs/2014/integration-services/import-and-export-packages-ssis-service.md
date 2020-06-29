---
title: 导入和导出包（SSIS 服务） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], importing
- packages [Integration Services], exporting
- importing packages
- exporting packages
ms.assetid: ef18ec11-b536-47d9-abd1-794099f43486
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 442a5580e81de39ac9786f692620e92327634138
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436904"
---
# <a name="import-and-export-packages-ssis-service"></a>导入和导出包（SSIS 服务）
    
> [!IMPORTANT]  
>  本主题论述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支持该服务以便与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的早期版本向后兼容。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 包既可以保存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 数据库的 sysssispackages 表中，也可以保存在文件系统中。  
  
 包存储区是 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务监视和管理的逻辑存储区，它包括在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的配置文件中指定的 msdb 数据库和文件系统。  
  
 您可以在下列存储类型之间导入和导出包：  
  
-   文件系统中任意位置的文件系统文件夹。  
  
-   SSIS 包存储区中的文件夹。 这两个默认文件夹分别称为“文件系统”和“MSDB”。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 数据库。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了导入和导出包的功能，通过此功能可以更改包的存储格式和位置。 使用导入和导出功能，您可以将包添加到文件系统、包存储区或 msdb 数据库，然后将包从一种存储格式复制为另一种存储格式。 例如，保存在 msdb 中的包可以复制到文件系统中，反之亦然。  
  
 还可以使用 **dtutil** 命令提示实用工具 (dtutil.exe) 将包复制为其他格式。 有关详细信息，请参阅 [dtutil Utility](dtutil-utility.md)。  
  
## <a name="to-import-or-export-a-package"></a>导入或导出包  
  
> [!IMPORTANT]  
>  本主题讨论作为 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的一部分的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]服务。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支持 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务以便与 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]向后兼容。 有关在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中管理包的信息，请参阅 [Integration Services (SSIS) 服务器](catalog/integration-services-ssis-server-and-catalog.md)。  
  
 您可以从以下位置导出 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包，或将包导入以下位置：  
  
-   您可以导入存储在实例 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 、文件系统或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区中的包。 导入的包将保存至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区中的文件夹。  
  
-   可以将存储在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例、文件系统或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区中的包导出至不同的存储格式和位置。  
  
 但对于在不同版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]之间导入和导出包，存在一些限制：  
  
-   对于 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]实例，可以从 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]实例导入包，但不能将包导出到 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]实例。  
  
-   对于 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]实例，不能从 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]实例导入包，也不能将包导出到该实例。  
  
 下列过程说明如何使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 导入或导出包。  
  
#### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 导入包  
  
1.  单击“开始”****，指向 Microsoft**** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，然后单击“SQL Server Management Studio”****。  
  
2.  在 **“连接到服务器”** 对话框中，设置以下选项：  
  
    -   在 **“服务器类型”** 框中，选择 **“Integration Services”**。  
  
    -   在 "**服务器名称**" 框中，提供服务器名称或单击 **\<Browse for more...>** 并找到要使用的服务器。  
  
3.  如果对象资源管理器未打开，请在 **“视图”** 菜单上，单击 **“对象资源管理器”**。  
  
4.  在对象资源管理器中，展开 **“已存储的包”** 文件夹。  
  
5.  展开子文件夹，找到要向其中导入包的文件夹。  
  
6.  右键单击该文件夹，单击“导入包”。**** 然后请执行下列操作之一：  
  
    -   若要从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的实例导入，请选择 **“SQL Server”** 选项，然后指定服务器并选择身份验证模式。 如果选择 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，请提供用户名和密码。  
  
         单击浏览按钮 **（...）**，选择要导入的包，然后单击 **"确定"。**  
  
    -   若要从文件系统导入，请选择 **“文件系统”** 选项。  
  
         单击浏览按钮 **（...）**，选择要导入的包，然后单击 "打开" **。**  
  
    -   若要从 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区中导入，请选择 **“SSIS 包存储区”** 选项，并指定服务器。  
  
         单击浏览按钮 **（...）**，选择要导入的包，然后单击 **"确定"。**  
  
7.  根据需要，也可以更新包名称。  
  
8.  若要更新包的保护级别，请单击浏览按钮 (…)，然后使用“包保护级别”对话框选择其他保护级别********。 如果选定了 **“使用密码加密敏感数据”** 或 **“使用密码加密所有数据”** 选项，请键入并确认密码。  
  
9. 单击 **“确定”** ，完成导入操作。  
  
#### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 导出包  
  
1.  单击“开始”****，指向 Microsoft**** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，然后单击“SQL Server Management Studio”****。  
  
2.  在 "**连接到服务器**" 对话框中，设置以下选项：  
  
    -   在 **“服务器类型”** 框中，选择 **“Integration Services”**。  
  
    -   在 "**服务器名称**" 框中，提供服务器名称或单击 **\<Browse for more...>** 并找到要使用的服务器。  
  
3.  如果对象资源管理器未打开，请在 **“视图”** 菜单上，单击 **“对象资源管理器”**。  
  
4.  在对象资源管理器中，展开 **“已存储的包”** 文件夹。  
  
5.  展开子文件夹以找到要导出的包。  
  
6.  右键单击该包，单击“导出”****，然后执行以下操作之一：  
  
    -   若要导出到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的实例，请选择 **SQL Server** 选项，然后指定服务器并选择身份验证模式。 如果选择 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，请提供用户名和密码。  
  
         单击浏览按钮 (…)，展开“SSIS 包”文件夹以找到要存储此包的文件夹********。 也可以更新此包的默认名称，然后单击 **“确定”**。  
  
    -   要导出到文件系统，请选择 **“文件系统”** 选项。  
  
         单击浏览按钮 (…) 以查找要向其中导出包的文件夹，键入包文件的名称，然后单击“保存”********。  
  
    -   若要导出到 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区，请选择 **“SSIS 包存储区”** 选项并指定服务器。  
  
         单击浏览按钮 (…)，展开“SSIS 包”文件夹，然后选择要存储此包的文件夹********。 也可以在 **“包名称”** 文本框中为包键入新名称。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  若要更新包的保护级别，请单击浏览按钮 (…)，然后使用“包保护级别”对话框选择其他保护级别********。 如果选定了 **“使用密码加密敏感数据”** 或 **“使用密码加密所有数据”** 选项，请键入并确认密码。  
  
8.  单击 **“确定”** ，完成导出操作。  
  
## <a name="see-also"></a>另请参阅  
 [包管理（SSIS 服务）](service/package-management-ssis-service.md)  
  
  
