---
title: 添加、 删除或共享连接管理器在包中 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], adding
- adding connection managers
ms.assetid: 6f2ba4ea-10be-4c40-9e80-7efcf6ee9655
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fdcc6285ba1a75827f91f856319d296c0cbbff5d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391685"
---
# <a name="add-delete-or-share-a-connection-manager-in-a-package"></a>在包中添加、删除或共享连接管理器
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括用于连接到不同数据源的多种连接管理器。这些数据源包括关系数据库、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库以及 CSV 和 XML 格式的文件。 可以在包级别或项目级别创建连接管理器。 在项目级别创建的连接管理器对项目中的所有包可用。 而在包级别创建的连接管理器对该特定包可用。  
  
 您使用在项目级别创建的连接管理器来替代数据源将连接共享到源。 要添加项目级别的连接管理器， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目必须使用项目部署模型。 将一个项目配置为使用此模型时， **“连接管理器”** 文件夹显示在 **“解决方案资源管理器”** 中，而 **“数据源”** 文件夹则从 **“解决方案资源管理器”** 中删除。  
  
> [!NOTE]  
>  如果您要使用包中的数据源，需要将项目转换为包部署模型。  
>   
>  有关两种模型的详细信息，请参阅 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)。 有关将项目转换为项目部署模型的详细信息，请参阅 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
 以下过程适用于所有连接管理器类型并说明如何执行以下任务：  
  
-   [若要创建包时添加连接管理器](#wizard)  
  
-   [若要向现有包中添加连接管理器](#package)  
  
-   [若要在项目级别添加连接管理器](#project)  
  
-   [若要创建连接管理器属性的参数](#parameter)  
  
-   [若要从包中删除连接管理器](#DeletePackageLevel)  
  
-   [若要删除共享的连接管理器 （项目级别连接管理器）](#DeleteProjectLevel)  
  
##  <a name="wizard"></a> 若要创建包时添加连接管理器  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导  
  
     除了创建和配置连接管理器之外，该向导还有助于创建和配置使用该连接管理器的源和目标。 有关详细信息，请参阅 [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)。  
  
##  <a name="package"></a> 若要向现有包中添加连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在“解决方案资源管理器”中，双击该包将其打开  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“控制流”** 选项卡、 **“数据流”** 选项卡或 **“事件处理程序”** 选项卡，以使 **“连接管理器”** 区域可用。  
  
4.  右键单击“连接管理器”区域中的任意位置，然后执行下列操作之一：  
  
    -   单击要添加到包中的连接管理器类型。  
  
         -或-  
  
    -   如果没有列出您要添加的类型，请单击 **“新建连接”** 打开 **“添加 SSIS 连接管理器”** 对话框，选择某种连接管理器类型，然后单击 **“确定”**。  
  
     随即打开与所选连接管理器类型对应的自定义对话框。 有关连接管理器类型以及可用选项的详细信息，请参阅下面的选项表。  
  
    |“ODBC 源编辑器”|选项|  
    |------------------------|-------------|  
    |[ADO 连接管理器](connection-manager/ado-connection-manager.md)|[配置 OLE DB 连接管理器](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 连接管理器](connection-manager/ado-net-connection-manager.md)|[配置 ADO.NET 连接管理器](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 连接管理器](connection-manager/analysis-services-connection-manager.md)|[“添加 Analysis Services 连接管理器”对话框 UI 参考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 连接管理器](connection-manager/excel-connection-manager.md)|[Excel 连接管理器编辑器](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[文件连接管理器](connection-manager/file-connection-manager.md)|[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[多文件连接管理器](connection-manager/multiple-files-connection-manager.md)|[“添加文件连接管理器”对话框 UI 参考](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[平面文件连接管理器](connection-manager/flat-file-connection-manager.md)|[平面文件连接管理器编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)<br /><br /> [平面文件连接管理器编辑器（“列”页）](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [平面文件连接管理器编辑器（“高级”页）](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [平面文件连接管理器编辑器（“预览”页）](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[多平面文件连接管理器](connection-manager/multiple-flat-files-connection-manager.md)|[多平面文件连接管理器编辑器（“常规”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多平面文件连接管理器编辑器（“列”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多平面文件连接管理器编辑器（“高级”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多平面文件连接管理器编辑器（“预览”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 连接管理器](connection-manager/ftp-connection-manager.md)|[FTP 连接管理器编辑器](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 连接管理器](connection-manager/http-connection-manager.md)|[HTTP 连接管理器编辑器（“服务器”页）](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 连接管理器编辑器（“代理”页）](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 连接管理器](connection-manager/msmq-connection-manager.md)|[MSMQ 连接管理器编辑器](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 连接管理器](connection-manager/odbc-connection-manager.md)|[ODBC 连接管理器 UI 参考](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 连接管理器](connection-manager/ole-db-connection-manager.md)|[配置 OLE DB 连接管理器](configure-ole-db-connection-manager.md)|  
    |[SMO 连接管理器](connection-manager/smo-connection-manager.md)|[SMO 连接管理器编辑器](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 连接管理器](connection-manager/smtp-connection-manager.md)|[SMTP 连接管理器编辑器](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 连接管理器](connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 连接管理器编辑器（“连接”页）](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 连接管理器编辑器（“全部”页）](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 连接管理器](connection-manager/wmi-connection-manager.md)|[WMI 连接管理器编辑器](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     **“连接管理器”** 区域列出已添加的连接管理器。  
  
5.  还可以右键单击连接管理器，单击“重命名”，然后修改连接管理器的默认名称。  
  
6.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
##  <a name="project"></a> 若要在项目级别添加连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中打开 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在“解决方案资源管理器”中，右键单击“连接管理器”单击“新建连接管理器”。  
  
3.  在 **“添加 SSIS 连接管理器”** 对话框中，选择连接管理器的类型，然后单击 **“添加”**。  
  
     随即打开与所选连接管理器类型对应的自定义对话框。 有关连接管理器类型以及可用选项的详细信息，请参阅下面的选项表。  
  
    |“ODBC 源编辑器”|选项|  
    |------------------------|-------------|  
    |[ADO 连接管理器](connection-manager/ado-connection-manager.md)|[配置 OLE DB 连接管理器](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 连接管理器](connection-manager/ado-net-connection-manager.md)|[配置 ADO.NET 连接管理器](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 连接管理器](connection-manager/analysis-services-connection-manager.md)|[“添加 Analysis Services 连接管理器”对话框 UI 参考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 连接管理器](connection-manager/excel-connection-manager.md)|[Excel 连接管理器编辑器](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[文件连接管理器](connection-manager/file-connection-manager.md)|[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[多文件连接管理器](connection-manager/multiple-files-connection-manager.md)|[“添加文件连接管理器”对话框 UI 参考](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[平面文件连接管理器](connection-manager/flat-file-connection-manager.md)|[平面文件连接管理器编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)<br /><br /> [平面文件连接管理器编辑器（“列”页）](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [平面文件连接管理器编辑器（“高级”页）](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [平面文件连接管理器编辑器（“预览”页）](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[多平面文件连接管理器](connection-manager/multiple-flat-files-connection-manager.md)|[多平面文件连接管理器编辑器（“常规”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多平面文件连接管理器编辑器（“列”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多平面文件连接管理器编辑器（“高级”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多平面文件连接管理器编辑器（“预览”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 连接管理器](connection-manager/ftp-connection-manager.md)|[FTP 连接管理器编辑器](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 连接管理器](connection-manager/http-connection-manager.md)|[HTTP 连接管理器编辑器（“服务器”页）](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 连接管理器编辑器（“代理”页）](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 连接管理器](connection-manager/msmq-connection-manager.md)|[MSMQ 连接管理器编辑器](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 连接管理器](connection-manager/odbc-connection-manager.md)|[ODBC 连接管理器 UI 参考](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 连接管理器](connection-manager/ole-db-connection-manager.md)|[配置 OLE DB 连接管理器](configure-ole-db-connection-manager.md)|  
    |[SMO 连接管理器](connection-manager/smo-connection-manager.md)|[SMO 连接管理器编辑器](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 连接管理器](connection-manager/smtp-connection-manager.md)|[SMTP 连接管理器编辑器](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 连接管理器](connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 连接管理器编辑器（“连接”页）](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 连接管理器编辑器（“全部”页）](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 连接管理器](connection-manager/wmi-connection-manager.md)|[WMI 连接管理器编辑器](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     您添加的连接管理器将显示在 **“解决方案资源管理器”** 中的 **“连接管理器”** 节点下。 它还将显示在项目中所有包的 **“SSIS 设计器”** 窗口的 **“连接管理器”** 选项卡中。 此选项卡中的连接管理器名称具有 **(project)** 前缀，以便将此项目级别的连接管理器与包级别的连接管理器区别开来。  
  
4.  或者，在“解决方案资源管理器”窗口中的“连接管理器”节点下或在“SSIS 设计器”窗口的“连接管理器”选项卡中，右键单击连接管理器，再单击“重命名”，然后修改连接管理器的默认名称。  
  
    > [!NOTE]  
    >  在“SSIS 设计器”窗口的“连接管理器”选项卡中，不能覆盖连接管理器名称中的 (project) 前缀。 这是设计的结果。  
  
##  <a name="parameter"></a> 若要创建连接管理器属性的参数  
  
1.  在“连接管理器”区域中，右键单击要为其创建参数的连接管理器，然后单击“参数化”。  
  
2.  在 **“参数化”** 对话框中配置参数设置。 有关详细信息，请参阅 [Parameterize Dialog Box](../../2014/integration-services/parameterize-dialog-box.md)。  
  
##  <a name="DeletePackageLevel"></a> 若要从包中删除连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“控制流”** 选项卡、 **“数据流”** 选项卡或 **“事件处理程序”** 选项卡，以使 **“连接管理器”** 区域可用。  
  
4.  右键单击要删除的连接管理器，然后单击“删除”。  
  
     如果删除包元素（例如执行 SQL 任务或 OLE DB 源）使用的连接管理器，您会得到以下结果：  
  
    -   使用已删除的连接管理器的包元素上会出现错误图标。  
  
    -   包验证失败。  
  
    -   包无法运行。  
  
5.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
##  <a name="DeleteProjectLevel"></a> 若要删除共享的连接管理器 （项目级别连接管理器）  
  
1.  若要删除项目级别的连接管理器，请在“解决方案资源管理器”窗口的“连接管理器”节点下，右键单击连接管理器，然后单击“删除”。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 显示下面的警告消息：  
  
    > [!WARNING]  
    >  在您删除某一项目连接管理器后，使用该连接管理器的包可能会不运行。 不能撤消此操作。 是否要删除该连接管理器?  
  
2.  单击“确定”将删除该连接管理器，单击“取消”将保留它。  
  
    > [!NOTE]  
    >  您也可以从为项目中任何包打开的 **“SSIS 设计器”** 窗口的 **“连接管理器”** 选项卡中删除项目级别的连接管理器。 为此，右键单击此选项卡中的连接管理器，然后单击“删除”。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 连接](connection-manager/integration-services-ssis-connections.md)   
 [设置连接管理器的属性](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
  
