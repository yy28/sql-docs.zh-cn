---
title: Integration Services 项目转换向导 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.migrationwizard.f1
ms.assetid: a192b094-4d0f-4c21-b911-460ec844a49f
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c00c15a0f5e1c6bc45dbf1d19c216feb468e41fe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194907"
---
# <a name="integration-services-project-conversion-wizard"></a>Integration Services 项目转换向导
  **“Integration Services 项目转换向导”** 可以将项目转换为项目部署模型。  
  
> [!NOTE]  
>  如果项目包含一个或多个数据源，则在项目转换完成时删除数据源。 若要创建到可由项目中的包共享的数据源的连接，请在项目级别添加连接管理器。 有关详细信息，请参阅 [Add, Delete, or Share a Connection Manager in a Package](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)。  
  
 **您希望做什么？**  
  
-   [打开“Integration Services 项目转换向导”](#open_dialog)  
  
-   [设置“查找包”页上的选项](#locate)  
  
-   [设置“选择包”页上的选项](#selectPackages)  
  
-   [设置“选择目标”页上的选项](#destination)  
  
-   [设置“指定项目属性”页上的选项](#projectProperties)  
  
-   [设置“更新执行包任务”页上的选项](#executePackage)  
  
-   [设置“选择配置”页上的选项](#configurations)  
  
-   [设置“创建参数”页上的选项](#createParameters)  
  
-   [设置“配置参数”页上的选项](#configureParameters)  
  
-   [设置“检查”页上的选项](#review)  
  
-   [设置执行转换的选项](#conversion)  
  
##  <a name="open_dialog"></a> 打开“Integration Services 项目转换向导”  
 执行下列操作之一以打开 **“Integration Services 项目转换”** 向导。  
  
-   在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中打开该项目，然后在解决方案资源管理器中，右键单击该项目并单击“转换为项目部署模型”。  
  
-   从 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 的对象资源管理器中，右键单击“项目”节点并选择“导入包”。  
  
 根据您是从 **还是从** 运行 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] “Integration Services 项目转换向导” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，该向导将执行不同的转换任务。 有关详细信息，请参阅 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
##  <a name="locate"></a> 设置“查找包”页上的选项  
  
> [!NOTE]  
>  只有在从 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]运行该向导时，“查找包”页才可用。  
  
 在“源”下拉列表中选择“文件系统”时，该页显示以下选项。 当包驻留在文件系统中时选择此选项。  
  
 **文件夹**  
 键入包路径，或通过单击“浏览”导航到该包。  
  
 在“源”下拉列表中选择“SSIS 包存储区”时，该页显示以下选项。 有关包存储区的详细信息，请参阅[包管理（SSIS 服务）](service/package-management-ssis-service.md)。  
  
 **Server**  
 键入服务器名称或选择该服务器。  
  
 **文件夹**  
 键入包路径，或通过单击“浏览”导航到该包。  
  
 在“源”下拉列表中选择“Microsoft SQL Server”时，该页显示以下选项。 当包驻留在 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中时选择此选项。  
  
 **Server**  
 键入服务器名称或选择该服务器。  
  
 **使用 Windows 身份验证**  
 Microsoft Windows 身份验证模式允许用户通过 Windows 用户帐户进行连接。 如果使用 Windows 身份验证，则不需要提供用户名或密码。  
  
 **使用 SQL Server 身份验证**  
 当户使用指定的登录名和密码从不可信连接进行连接时， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将通过检查是否已设置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录帐户以及指定的密码是否与以前记录的密码匹配，对该连接进行身份验证。 如果未设置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录帐户，则身份验证失败，并且用户会收到一条错误消息。  
  
 **用户名**  
 使用 SQL Server 身份验证时，指定用户名。  
  
 **密码**  
 使用 SQL Server 身份验证时，提供密码。  
  
 **文件夹**  
 键入包路径，或通过单击“浏览”导航到该包。  
  
##  <a name="selectPackages"></a> 设置“选择包”页上的选项  
 **包名称**  
 列出包文件。  
  
 **“状态”**  
 指示包是否已准备好转换为项目部署模型。  
  
 **Message**  
 显示与包关联的消息。  
  
 **密码**  
 显示与包关联的密码。 密码文本将被隐藏。  
  
 **应用于所选内容**  
 单击以将“密码”文本框中的密码应用于一个或多个所选包。  
  
 **“刷新”**  
 刷新包的列表。  
  
##  <a name="destination"></a> 设置“选择目标”页上的选项  
 在此页上，指定新的项目部署文件 (.ispac) 的名称和路径或者选择一个现有文件。  
  
> [!NOTE]  
>  只有在从 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 运行该向导时，“选择目标”页才可用。  
  
 **输出路径**  
 键入部署文件的路径，或通过单击“浏览”导航到该文件。  
  
 **项目名称**  
 键入项目名称。  
  
 **保护级别**  
 选择保护级别。 有关详细信息，请参阅 [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md)。  
  
 **项目说明**  
 键入项目的可选说明。  
  
##  <a name="projectProperties"></a> 设置“指定项目属性”页上的选项  
  
> [!NOTE]  
>  只有在从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]运行该向导时，“指定项目属性”页才可用。  
  
 **项目名称**  
 列出项目名称。  
  
 **保护级别**  
 为项目中所含的包选择保护级别。 有关保护级别的详细信息，请参阅 [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md)。  
  
 **项目说明**  
 键入可选的项目说明。  
  
##  <a name="executePackage"></a> 设置“更新执行包任务”页上的选项  
 更新包中所含的执行包任务，以使用基于项目的引用。 有关详细信息，请参阅 [Execute Package Task Editor](../../2014/integration-services/execute-package-task-editor.md)。  
  
 **父包**  
 列出使用执行包任务执行子包的包名称。  
  
 **任务名称**  
 列出执行包任务的名称。  
  
 **原始引用**  
 列出子包的当前路径。  
  
 **分配引用**  
 选择存储在项目中的子包。  
  
##  <a name="configurations"></a> 设置“选择配置”页上的选项  
 选择您要用参数替换的包配置。  
  
 **“包”**  
 列出包文件。  
  
 **类型**  
 列出配置类型，如 XML 配置文件。  
  
 **配置字符串**  
 列出配置文件的路径。  
  
 **“状态”**  
 显示配置的状态消息。 单击该消息可以查看整个消息文本。  
  
 **添加配置**  
 将在其他项目中包含的包配置添加到要用参数替换的可用配置的列表中。 您可以选择存储在文件系统或 SQL Server 中的配置。  
  
 **“刷新”**  
 单击以刷新配置列表。  
  
 **在转换后删除所有包的配置**  
 建议通过选择此选项从项目中删除所有配置。  
  
 如果您没有选择此选项，将只删除您已选择用参数替换的配置。  
  
##  <a name="createParameters"></a> 设置“创建参数”页上的选项  
 选择每个配置属性的参数名称和作用域。  
  
 **“包”**  
 列出包文件。  
  
 **参数名称**  
 列出参数名称。  
  
 **范围**  
 选择参数的作用域（包或项目）。  
  
##  <a name="configureParameters"></a> 设置“配置参数”页上的选项  
 **名称**  
 列出参数名称。  
  
 **范围**  
 列出参数的作用域。  
  
 **ReplTest1**  
 列出参数值。  
  
 单击值字段旁边的省略号按钮以配置参数属性。  
  
 在 **“设置参数详细信息”** 对话框中，可以编辑参数值。 还可以指定在运行包时是否必须提供参数值。  
  
 您可以通过单击参数旁的“浏览”按钮，在 **的** “配置” **对话框的** “参数” [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]页中修改值。 将显示 **“设置参数值”** 对话框。  
  
 **“设置参数详细信息”** 对话框还列出参数值的数据类型和参数的来源。  
  
##  <a name="review"></a> 设置“检查”页上的选项  
 使用 **“检查”** 页可以确认您为项目转换选择的选项。  
  
 **Previous**  
 单击以更改选项。  
  
 **转换**  
 单击以将项目转换为项目部署模型。  
  
##  <a name="conversion"></a> 设置执行转换的选项  
 “执行转换”页显示项目转换的状态。  
  
 **操作**  
 列出特定的转换步骤。  
  
 **结果**  
 列出每个转换步骤的状态。 单击状态消息可获取详细信息。  
  
 直到在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中保存项目后，才保存项目转换。  
  
 **保存报告**  
 单击以在 .xml 文件中保存项目转换的摘要。  
  
## <a name="see-also"></a>请参阅  
 [将项目部署到 Integration Services 服务器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)  
  
  
