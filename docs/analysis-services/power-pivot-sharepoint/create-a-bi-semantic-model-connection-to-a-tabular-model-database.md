---
title: "创建 BI 语义模型连接到表格模型数据库 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 69b306f6-ee8a-44d2-8f51-0cad2c0bc135
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cad58c850f42e42791bbd57c010b48234e5640e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a>创建与表格模型数据库的 BI 语义模型连接
  使用本主题中的信息设置一个 BI 语义模型连接，该连接将重定向到在 SharePoint 场外的 Analysis Services 实例上运行的表格模型数据库。  
  
 在创建 BI 语义模型连接并配置 SharePoint Services 和 Analysis Services 权限后，可将其用作 Excel 或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报告的数据源。  
  
 本主题包含以下各节。 按给出的顺序执行每个任务。  
  
 [检查必备条件](#bkmk_prereq)  
  
 [授予对共享服务应用程序的 Analysis Services 管理权限](#bkmk_ssas)  
  
 [授予对表格模型数据库的读取权限](#bkmk_BISM)  
  
 [创建与表格模型数据库的 BI 语义模型连接](#bkmk_connect)  
  
 [配置 BI 语义模型连接的 SharePoint 权限](#bkmk_permissions)  
  
 [后续步骤](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> 检查必备条件  
 您必须具有“参与讨论”权限或更高权限以创建 BI 语义模型连接文件。  
  
 您必须具有支持 BI 语义模型连接内容类型的库。 有关详细信息，请参阅[将 BI 语义模型连接内容类型添加到库 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md)。  
  
 您必须知道将为其设置 BI 语义模型连接的服务器和数据库名称。 必须为表格模式配置 Analysis Services。 服务器上运行的数据库必须是表格模型数据库。 有关如何检查服务器模式的说明，请参阅 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
 在某些情况下，SharePoint 环境下的共享服务必须对 Analysis Services 实例具有管理权限。 这些服务包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序、Reporting Services 服务应用程序和 PerformancePoint 服务应用程序。 您必须首先知道这些服务应用程序的标识，然后才能授予管理权限。 您可以使用管理中心来确定标识。  
  
 您必须是 SharePoint 服务管理员才能查看管理中心内的安全信息。  
  
 您必须是 Analysis Services 系统管理员才能授予 Management Studio 中的管理权限。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint。 外部数据源的 BI 语义模型连接依赖于经典模式登录。 有关详细信息，请参阅 [Power Pivot Authentication and Authorization](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md)。  
  
 参与连接序列的所有计算机和用户都必须处于同一个域或可信域（双向信任）中。  
  
##  <a name="bkmk_ssas"></a> 授予对共享服务应用程序的 Analysis Services 管理权限  
 SharePoint 与 Analysis Services 服务器上的表格模型数据库之间的连接有时候是由共享服务代表请求数据的用户建立的。 发出请求的服务可以是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序、Reporting Services 服务应用程序或 PerformancePoint 服务应用程序。 为了能成功连接，该服务必须拥有 Analysis Services 服务器的管理权限。 在 Analysis Services 中，仅管理员能够代表其他用户建立模拟连接。  
  
 在以下条件下使用连接时需要管理权限：  
  
-   在配置 BI 语义模型连接文件的过程中验证连接信息时。  
  
-   在使用 BI 语义模型连接启动 Power View 报表时。  
  
-   在使用 BI 语义模型连接填充 PerformancePoint Web 部件时。  
  
 为了确保这些行为按预期执行，请在 Analysis Services 实例上向各服务标识授予管理权限。 使用以下说明授予所需权限。  
  
 **将服务标识添加到服务器管理员角色**  
  
1.  在 SQL Server Management Studio 中，连接到 Analysis Services 实例。  
  
2.  右键单击服务器名称并选择“属性”。  
  
3.  单击 **“安全性”**，然后单击 **“添加”**。 输入用于运行服务应用程序的 Windows 用户帐户。  
  
     您可以使用管理中心来确定标识。 在“安全性”部分中，打开 **“配置服务帐户”** 可查看与用于各应用程序的服务应用程序池关联的 Windows 帐户，然后，按照本主题中提供的说明执行，以便向帐户授予管理权限。  
  
##  <a name="bkmk_BISM"></a> 授予对表格模型数据库的读取权限  
 由于数据库在服务器场外部的服务器上运行，因此设置您的连接的部分工作是授予后端 Analysis Services 服务器的数据库用户权限。 Analysis Services 使用基于角色的权限模型。 连接到模型数据库的用户必须具有读取权限或更高权限并且通过对其成员授予读取读取访问权限的角色才能执行此操作。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建模型时会定义角色（有时会定义角色成员身份）。 虽然无法使用 SQL Server Management Studio 创建角色，但可以使用它向已定义的角色中添加成员。 有关创建角色的详细信息，请参阅[创建和管理角色（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
#### <a name="assign-role-membership"></a>分配角色成员身份  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例，再在对象资源管理器中展开数据库，然后展开 **“角色”**。 您应看到已定义的角色。 如果角色不存在，请与模型作者联系并请求添加或角色。 必须先重新部署模型，然后角色才会显示在 Management Studio 中。  
  
2.  右键单击角色，然后选择“属性”。  
  
3.  在“成员身份”页中，添加要求访问权限的 Windows 组和用户帐户。  
  
##  <a name="bkmk_connect"></a> 创建与表格模型数据库的 BI 语义模型连接  
 在 Analysis Services 中设置权限后，您可以返回到 SharePoint 并创建 BI 语义模型连接。  
  
1.  在将包含 BI 语义模型连接的库中，单击 SharePoint 功能区上的 **“文档”** 。  
  
2.  单击“新建文档”上的向下箭头，然后选择 **“BI 语义模型连接文件”** 以打开“新建 BI 语义模型连接”页。  
  
3.  设置 **“服务器”** 和 **“数据库”** 属性。 如果您不确定数据库名称，则使用 SQL Server Management Studio 可以查看在服务器上部署的数据库的列表。  
  
     “服务器名称”为服务器的网络名称、IP 地址或完全限定域名（例如，myserver.mydomain.corp.adventure-works.com）。 如果服务器作为命名实例安装，则以 computername\instancename 格式输入服务器名称。  
  
     **数据库** 必须为服务器上当前可用的表格数据库。 不要指定其他 BI 语义模型连接文件、Office 数据连接 (.odc) 文件、Analysis Services OLAP 数据库或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿。 若要获取数据库名称，您可以使用 Management Studio 连接到服务器并查看可用数据库的列表。 使用数据库的属性页以确保您拥有正确的名称。  
  
4.  单击 **“确定”** 保存该页。 此时， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序会验证连接。  
  
     如果连接信息正确，并且你向 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序授予了管理权限，以便它可以作为当前用户连接到 Analysis Services，则验证成功。  
  
     如果连接信息错误或服务应用程序缺少权限，验证将失败。 验证消息将在页面上出现，询问您是否要保存该文件。 如果您知道连接有效，则应保存该文件，因为错误是由于缺少权限导致的，而非连接信息无效。  
  
     您可以通过在 Excel 或 Power View 中使用该连接来连接到表格模型数据库，对连接进行验证。 如果数据源连接成功，则连接是有效的，尽管出现验证警告。  
  
##  <a name="bkmk_permissions"></a> 配置 BI 语义模型连接的 SharePoint 权限  
 为了能够使用 BI 语义模型连接作为 Excel 工作簿或 Reporting Services 报表的数据源，需要针对 SharePoint 库中 BI 语义模型连接项的 **“读取”** 权限。 该“读取”权限级别包括 **“打开项”** 权限，该权限支持将 BI 语义模型连接信息下载到 Excel 桌面应用程序。  
  
 有几种方法可在 SharePoint 中授予权限。 下面的说明解释如何新建一个名为 **BISM Users** 的具有“读取”  权限级别的组。  
  
 您必须是网站所有者才能更改权限。  
  
1.  在“网站操作”中，单击 **“网站权限”**。  
  
2.  单击“创建组”  并将新组命名为 **BISM Users**。  
  
3.  选择 **“读取”** 权限级别，然后单击 **“创建”**。  
  
4.  在“人员和组”中选择 **BISM Users** 。  
  
5.  指向“新建”，单击 **“添加用户”**，然后添加用户或组帐户。  
  
     此时，这些用户和组将拥有对整个网站的“读取”权限，包括从网站级别继承权限的所有库和列表。 如果这些权限太高，则可以选择从特定的库、列表或项中删除此组。  
  
 若要选择性地删除项目级别的权限，请执行以下操作：  
  
1.  在库中选择一个文档。 单击右下箭头，然后单击 **“管理权限”**。  
  
2.  默认情况下，项会继承权限。 若要更改此库中的单个文档的权限，请单击 **“停止继承权限”**。  
  
3.  选中 “BISM 用户”旁的复选框。  
  
4.  单击 **“删除用户权限”**。  
  
##  <a name="bkmk_next"></a> 后续步骤  
 创建了 BI 语义模型连接并且确保其安全后，可以将该连接指定为数据源。 有关详细信息，请参阅 [在 Excel 或 Reporting Services 中使用 BI 语义模型连接](../../analysis-services/power-pivot-sharepoint/use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [PowerPivot BI 语义模型连接 (.bism)](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [创建与 Power Pivot 工作簿的 BI 语义模型连接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
  
