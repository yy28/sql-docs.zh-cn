---
title: 保存包 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.savecopyas.f1
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 60dcf1692fb8b805b9eef8fad228353104131c93
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295740"
---
# <a name="save-packages"></a>保存包

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，通过使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器可以生成包，并将包作为 XML 文件（.dtsx 文件）保存到文件系统中。 还可以将包 XML 文件的副本保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 msdb 数据库，或保存到包存储区。 包存储区表示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务管理的文件系统位置中的文件夹。  
  
 如果将包保存到文件系统，则稍后可以使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务将包导入到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或包存储区。 有关详细信息，请参阅 [Integration Services 服务（SSIS 服务）](../integration-services/service/integration-services-service-ssis-service.md)。  
  
 还可以使用命令提示实用工具 **dtutil**在文件系统和 msdb 之间复制包。 有关详细信息，请参阅 [dtutil Utility](../integration-services/dtutil-utility.md)。  
## <a name="save-a-package-to-the-file-system"></a>将包保存到文件系统  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含要保存到文件的包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，单击要保存的包。  
  
3.  在 **“文件”** 菜单上单击 **“保存选定项”** 。  
  
    > [!NOTE]  
    >  可以在“属性”窗口中验证保存包的路径及文件名。  

## <a name="save-a-copy-of-a-package"></a>保存一个包副本
  此部分介绍如何将包的副本保存到文件系统、包存储区或   中的 msdb 数据库[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 指定保存包副本的位置时，也能够更新包的名称。  
  
 包存储区可以同时包括 **msdb** 数据库和文件系统中的文件夹，也可以只包含 **msdb**或文件系统中的文件夹。 在 **msdb**中，包将保存到 **sysssispackages** 表中。 此表包括一个 **folderid** 列，用于标识包所属的逻辑文件夹。 逻辑文件夹提供了对保存到 **msdb** 中的包进行分组的有用方式，文件系统中的文件夹也提供了对保存到文件系统中的包进行分组的方式。 **msdb** 中的 **sysssispackagefolders** 表中的行定义这些文件夹。  
  
 在没有将 **msdb** 定义为包存储区的一部分的情况下，如果在 **“包路径”** 选项中选择 SQL Server，则可以继续使包与现有逻辑文件夹关联。  
  
> [!NOTE]  
>  在保存包的副本之前，必须在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开包。  
  
### <a name="to-save-a-copy-of-a-package"></a>保存包的副本  
  
1.  在解决方案资源管理器中，双击要保存其副本的包。  
  
2.  在“文件”菜单上，单击“包文件**的副本 > 另存为”** **\<** 。  
  
3.  在 **“保存包的副本”** 对话框，在 **“包位置”** 列表中选择包的位置。 提供了以下选项：  
    -   SQL Server
    -   文件系统 
    -   SSIS 包存储区 
  
4.  如果位置为 **SQL Server** 或 **“SSIS 包存储区”** ，请提供服务器名称。  
  
5.  如果保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请指定身份验证类型；如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，还请提供用户名和密码。  
  
6.  若要指定包路径，请键入路径或单击浏览按钮 (…)，以指定包的位置  。 包的默认名称为 Package。 也可以将包名称更新为所需的名称。  
  
     如果选择 **SQL Server** 作为 **“包路径”** 选项，则包路径由 **msdb** 中的逻辑文件夹和包名称构成。 例如，如果包 DownloadMonthlyData 与 MSDB 文件夹中的 Finance 文件夹（ **msdb**中的根逻辑文件夹的默认名称）相关联，则名为 DownloadMonthlyData 的包的包路径为 MSDB/Finance/DownloadMonthlyData  
  
     如果选择 **“SSIS 包存储区”** 作为 **“包路径”** 选项，则包路径由 Integration Services 服务管理的文件夹构成。 例如，如果包 UpdateDeductions 位于该服务所管理的文件系统文件夹中的 HumanResources 文件夹内，则包路径为 /File System/HumanResources/UpdateDeductions；同样，如果包 PostResumes 与 MSDB 文件夹中的 HumanResources 文件夹关联，则包路径为 MSDB/HumanResources/PostResumes。  
  
     如果选择 **“文件系统”** 作为 **“包路径”** 选项，则包路径为文件系统中的位置和文件名。 例如，如果包名称为 UpdateDemographics，则包路径为 C:\HumanResources\Quarterly\UpdateDemographics.dtsx。  
  
7.  查看包保护级别。  
  
8.  还可以单击“保护级别”旁边的 (…) 浏览按钮，更改保护级别   。  
  
    -   在 **“包保护级别”** 对话框中，选择不同的保护级别。  
  
    -   单击“确定”。   
  
9. 单击“确定”。   

## <a name="save-a-package-as-a-package-template"></a>将包保存为包模板
 本部分介绍在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中创建新的 Integration Services 包时如何制定自定义包以及将自定义包作为模板。 默认情况下，在将新包添加到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中时， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 使用创建空包的包模板。 您无法替换此默认模板，但可以添加新的模板。  
  
 可以指定多个包用作模板。 必须先创建这些包，然后才能实现将自定义包作为模板。  
  
 使用自定义包作为模板来创建包时，新的包将具有与模板相同的名称和 GUID。 若要区分这些包，应当更新 **Name** 属性的值，并为 **ID** 属性生成新的 GUID。 有关详细信息，请参阅 [在 SQL Server Data Tools 中创建包](../integration-services/create-packages-in-sql-server-data-tools.md) 和 [设置包属性](../integration-services/set-package-properties.md)。  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>将自定义包指定为包模板  
  
1.  在文件系统中，找到要用作模板的包。  
  
2.  将此包复制到 DataTransformationItems 文件夹中。 默认情况下，此文件夹位于 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject。  
  
3.  对每个要用作模板的包重复步骤 1 和 2。  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>使用自定义包作为包模板  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要在其中创建包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击项目，指向“添加”，然后单击“新建项”。    
  
3.  在“添加新项 —**项目名称>”对话框中，单击要用作模板的包\<** 。  
  
     模板列表包括名为“新建 SSIS 包”的默认包模板。 包图标将标识可以用作包模板的模板。  
  
4.  单击“添加”  。  
