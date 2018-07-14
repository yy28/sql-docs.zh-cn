---
title: 在 SharePoint 站点上的报表查看器 Web 部件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: b6341a73-172f-4632-a9e9-cc79fed3f36b
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 87498b7eca136eba037a8454416b875f5690cae3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198477"
---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>在 SharePoint 站点上的报表查看器 Web 部件
  报表查看器 Web 部件是由用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序安装的自定义 Web 部件。 您可以使用该 Web 部件查看、导航、打印和导出配置为在 SharePoint 集成模式下运行的报表服务器上的报表。 报表查看器 Web 部件是由处理的报表定义 (.rdl) 文件与相关联[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报表服务器。 不能将该部件与在其他软件产品中创建的其他报表文档一起使用。  
  
 若要安装该 Web 部件，必须运行 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序的安装程序。 您不应单独安装或卸载该 Web 部件。 它是外接程序的一部分，只能通过外接程序安装包进行安装。 报表查看器 Web 部件文件名为 ReportViewer.dwp。 该文件位于 Program Files\Common Files\Microsoft Shared\web server extensions\12\template\features\reportserver 文件夹，并且不应移到其他文件夹中。  
  
 若要使用该 Web 部件，必须已经安装和配置 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序并已将报表服务器配置为 SharePoint 集成。 还必须具有要在查看器中显示的报表。 您只能打开库、库文件夹、报表历史记录中的报表或从库 Web 部件到报表查看器 Web 部件的链接中的报表。 不能打开另存为自定义列表项的附件的报表。  
  
 您可以设置报表查看器 Web 部件的属性，从而控制工具栏和视图区域的外观并将该 Web 部件链接到特定报表。 报表查看器将显示显式链接到它的报表，或者显示打开的任何 .rdl 文件。  
  
 不能将多个报表链接到单个报表查看器实例，但是如果希望将这些报表组合在一起，则可以创建在单页上嵌入多个报表查看器 Web 部件实例的面板或 Web 部件页。  
  
 该 Web 部件包括视图区域、工具栏、用于设置凭据和参数的可折叠区域，以及属性。 下图显示了包含 Company Sales 示例报表以及可从工具栏中选择的导出选项的 Web 部件。  
  
 ![报表查看器 Web 部件](media/rs-sharepointrvwebpart.gif "报表查看器 Web 部件")  
  
## <a name="web-part-components"></a>Web 部件组件  
 视图区域以 HTML 格式显示报表。 根据 Web 部件的配置方式，视图区域可能会最大化以整页模式显示报表，或者可能与相邻窗格和工具栏共享可用空间。  
  
 工具栏提供页面导航、搜索、缩放和导出功能，以便您能以其他应用程序格式查看报表。 它还提供可选的打印功能，可为 HTML 报表提供分页打印输出并能更改页面布局和边距设置。 工具栏上的 **“操作”**, **“使用报表生成器打开”**、“订阅”、 **“导出”** 和 **“打印”** 。 页面导航和缩放控件直接位于工具栏上。  
  
> [!NOTE]  
>  您不能自定义工具栏，除非编写代码来执行此操作，但可以设置属性以全部或部分隐藏工具栏的控件。  
  
### <a name="export-action-on-the-report-toolbar"></a>报表工具栏上的导出操作  
 **“操作”** 菜单上的 **“导出”** 显示与报表服务器上所部署的呈现扩展插件相关联的应用程序格式。 若要确定特定格式的可用性，可以在报表服务器上添加或删除呈现扩展插件，也可以修改配置设置以删除列表中的特定导出格式。 还可以在报表服务器上指定配置设置以控制哪些格式可用。 通过添加和修改某一特定呈现扩展插件的配置设置，可以修改相应格式的默认行为。  
  
### <a name="print-action-on-the-report-toolbar"></a>报表工具栏上的打印操作  
 **打印**上**操作**菜单，通过提供的自定义打印功能[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]。 当您单击**打印**，ActiveX 客户端打印控件将下载到客户端计算机。 大多数情况下，单击 **“打印”** 的用户必须拥有本地计算机的管理员权限。 常见的做法是仅允许拥有管理员权限的用户下载 ActiveX 控件。 可以使用 SharePoint 管理中心启用或禁用客户端打印控件的下载。  
  
### <a name="find-action-on-the-report-toolbar"></a>报表工具栏上的查找操作  
 **“操作”** 菜单上的 **“查找”** 提供移动到报表中的目标位置的方法。 可以通过键入要查找的词或短语搜索报表内容。 搜索项的最大值为 256 个字符。 搜索在报表中查找匹配值时，焦点将移动到包含该值的报表部分。  
  
 输入要搜索的值时，键入您预计显示在报表中的值。 请不要提出“这个月的平均利润是多少”之类的问题，除非您预计该句中的每个词都显示在报表中。  
  
 一次只能搜索一个词或值。 不能使用搜索运算符（例如 `AND` 或 `OR`），也不能使用符号和通配符。 不能对数据的交叉部分执行搜索（例如，搜索特定产品在特定月份的净销售额）。 对于这种分析，请使用报表生成器来创建点击链接型报表。  
  
 限制访问报表数据的数据库和模型安全设置将应用于搜索操作。 如果您要在将模型作为数据源的点击链接型报表中搜索值，并且您没有对模型部分的访问权限，则由模型部分表示的数据将从搜索中排除。  
  
### <a name="panes-for-specifying-credentials-and-parameters"></a>用于指定凭据和参数的窗格  
 **“凭据”** 和 **“参数”** 窗格显示在视图区域旁边。 将报表的数据源连接配置为提示用户输入有权访问数据源的帐户和密码时将显示 **“凭据”** 。 报表接受报表中所定义参数的用户输入时将显示 **“参数”** 。  
  
### <a name="setting-properties-on-the-report-viewer-web-part"></a>设置报表查看器 Web 部件的属性  
 Web 部件的属性包括特定于报表查看器的自定义属性以及可以为任何 Web 部件设置的常规属性。 有关详细信息，请参阅[自定义报表查看器 Web 部件](../../2014/reporting-services/customize-the-report-viewer-web-part.md)。  
  
 默认情况下，报表以整页模式打开。 整页模式将显示可提供页面导航、搜索以及其他功能的工具栏。 您可以自定义 Web 部件来更改外观或默认行为。  
  
## <a name="see-also"></a>请参阅  
 [安装或卸载 Reporting Services 外接程序的 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [将报表查看器 Web 部件添加到 Web 页&#40;Reporting Services SharePoint 集成模式下&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
