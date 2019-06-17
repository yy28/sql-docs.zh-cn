---
title: 在 SharePoint 模式下 (SSRS) 报表服务器上的已发布的报表项的 URL 示例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 54cb861a-8cec-445c-875d-599fb9bd1973
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a7cbf3b3e6e378f27e5c56de6b043c95c56774f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099448"
---
# <a name="url-examples-for-published-report-items-on-a-report-server-in-sharepoint-mode-ssrs"></a>用于 SharePoint 模式下在报表服务器上已发布的报表项的 URL 示例 (SSRS)
  若要将报表和相关项发布到 SharePoint 库，可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 创作工具（如报表设计器）发布内容，或者使用 SharePoint 站点操作来上载内容。  
  
 SharePoint 站点使用的 Web 地址与本机模式下的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器的地址不同。 SharePoint 站点 Web 层次结构包括 SharePoint Web 应用程序、一个顶级站点和多个可选子站点以及库。 您必须知道如何创建 URL 地址，该地址指定 SharePoint 服务器以及 SharePoint 站点层次结构中的位置（您要在该位置发布报表或相关项）。  
  
 与报表有关的项包括共享数据源、子报表、钻取报表以及基于 Web 的图像文件等资源。 已发布到 SharePoint 库的报表必须通过它们在 SharePoint 库中的位置来指定这些相关项。  
  
 使用本主题中的示例可帮助创建指向您的报表解决方案中的报表和相关项的 URL。  
  
## <a name="site-hierarchy"></a>站点层次结构  
 将报表服务器配置为在 SharePoint 集成模式下运行时，SharePoint Web 层次结构将用于对在报表服务器上处理和管理的项进行寻址。  
  
 以下 Web 层次结构元素可用于访问和保护报表服务器内容。 其他对象（如列表和页）不用于访问报表服务器内容，因此未在下表中进行说明。  
  
|Object|Description|  
|------------|-----------------|  
|SharePoint Web 应用程序|SharePoint Web 应用程序可以作为独立的服务器安装，也可以在包含许多虚拟服务器的场中安装。 Web 应用程序具有 URL（例如，http: *//servername*）并且可以包含多个站点。|  
|站点|站点为 Web 应用程序的父站点或子站点。|  
|SharePoint 库|库包含文档或文件夹。 库或库中的文件夹是仅有的可用来存储报表、报表模型、共享数据源和外部图像的站点对象。|  
|项|可以在 URL 中引用的报表服务器项包括报表或子报表的报表定义、报表模型、共享数据源或外部图像。|  
  
## <a name="url-syntax-and-rules"></a>URL 语法和规则  
 库中每个报表服务器项都由完全限定的 URL 进行标识，该 URL 包括协议前缀、服务器名、站点、库、文件名和文件类型的文件扩展名。  
  
### <a name="url-for-a-sharepoint-server"></a>SharePoint 服务器的 URL  
 从 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 向报表服务器部署报表服务器或报表模型项目时，必须使用 SharePoint 服务器的 URL。  
  
 若要找到要使用的服务器的名称，请打开一个浏览器并找到要发布报表的 SharePoint 库。 服务器名称紧接在协议前缀之后，例如 http: *//servername*。  
  
 不支持使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 代理端点。 代理端点包含一个端口号，例如 http: *//servername:8080/reportserver*。  
  
### <a name="url-for-a-sharepoint-server-site-or-subsite"></a>SharePoint 服务器站点或子站点的 URL  
 部署报表或报表数据源时，必须使用 SharePoint 站点和子站点的 URL（如果有）。 在该 URL 中，站点名紧接在服务器名之后，例如 http://*servername/site* 或 http://*servername/site/subsite*。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Web 应用程序中，站点和子站点经常对应于主站点上的选项卡。 若要找到站点名或子站点名，请单击 **“主文件夹”** ，然后单击 **“所有网站内容”** 。 滚动到底部并查找 **“站点和工作区”** 。 站点列表将显示在此部分中。  
  
### <a name="url-for-a-sharepoint-library"></a>SharePoint 库的 URL  
 向 SharePoint 库中部署报表或相关项时，必须使用 SharePoint 库的 URL。 要用于库的 URL 根据所使用的 SharePoint 版本而不同。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 或 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]上，库显示在服务器名称之后，例如 http://*servername/* Shared Documents。  
  
 在 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]中，库显示在站点和子站点之后。 例如， http://*servername/site/* Documents。  
  
 若要查找新的 SharePoint 库或某个不熟悉站点的路径信息，请打开浏览器，然后找到要发布报表的 SharePoint 库。 如果该库为空，则上载任意文件。 右键单击该文件，然后选择“属性”以打开“属性”窗口   。 文件地址中包含发布操作所需的 URL 值。  
  
### <a name="fully-qualified-urls-for-items-on-a-sharepoint-site"></a>SharePoint 站点上的项的完全限定 URL  
 始终通过完全限定的 URL 对存储在 SharePoint 库中的项进行寻址，这种完全限定的 URL 以 Web 应用程序开头 (http://*server*) 作为根节点，并以所引用的文件名结束。  
  
 URL 中的文件名必须包括文件扩展名。  
  
 不能对发布到 SharePoint 站点的报表中的依赖项使用相对 URL。 例如，不能使用相对 URL 来引用共享数据源、报表模型或子报表。 必须始终为每个项指定 SharePoint 库的完全限定 URL。 无法预测依赖文件可能处于的位置，这是因为没有可以用来分析 URL 格式的站点预定义层次结构。  
  
 发布或上载包含依赖项的报表时，必须在发布报表后设置对依赖项的引用。 不能保证在报表设计器的预览模式下可以正常使用的引用在发布报表后还能够正常使用。 有关详细信息，请参阅本主题中的 [从创作工具发布到 SharePoint 库](#publishingToDocLib) 。  
  
### <a name="urls-for-external-images"></a>外部图像的 URL  
 报表定义可以包括存储为外部文件的图像文件。 可通过设置图像文件的完全限定 URL 来引用报表定义中的该文件。 该文件可以存储在 SharePoint 站点上，也可以存储在远程计算机上。  
  
> [!IMPORTANT]  
>  如果外部 URL 表示 SharePoint 网站上的图像，则在报表生成器中预览报表时将显示图像无效图标。 将报表上载到 SharePoint 站点并以连接模式呈现报表时，如果只有`View Items`权限，则将显示该图像无效图标。  
  
 无论采用何种报表服务器模式，在报表中对外部图像文件的引用必须为完全限定的 URL。 此外，引用外部图像文件通常会需要配置无人参与的报表处理帐户。  
  
### <a name="specifying-subreports-and-drillthrough-reports"></a>指定子报表和钻取报表  
 子报表必须与主报表位于同一文件夹。 不能指定相对文件夹。  
  
 若要指定钻取报表，请在表达式中包含 URL。 例如，若要将名为 SalesDetails 的报表指定为钻取报表，请在文本框或占位符文本的“操作”中，将 ReportName 设置为以下表达式：  
  
```  
="http://site/subsite/documentlibrary/SalesDetails.rdl"  
```  
  
### <a name="reserved-names-on-sharepoint-sites"></a>SharePoint 站点上的保留名称  
 如果要创建或构造位于 SharePoint 站点上的项的 URL，请注意： **Personal** 和 **Sites** 都是默认站点下的保留名称。  
  
## <a name="examples-of-urls"></a>URL 示例  
 将项发布到 SharePoint 库中时，必须指定目标库的完全限定 URL。 完全限定的 SharePoint URL 包括 SharePoint Web 应用程序、站点、库、文件夹（可选）、文件和文件扩展名。 以下示例对应使用的语法进行了一些说明：  
  
|目标|示例 URL|  
|------------|-----------------|  
|SharePoint 服务器。|http://TestServer|  
|SharePoint 服务器站点或子站点。|http://TestServer/toplevelsite/subsite|  
| 或 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 部署的 Shared Documents [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 中的 Company Sales 示例报表。|http://TestServer/TestSite/Shared%20Documents/Company%20Sales.rdl|  
|**或** 实例的 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] Documents/Doc [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 文件夹中的 Company Sales 示例报表。|http://TestServer/TestSite/Documents/Doc/Company%20Sales.rdl|  
| 或 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 实例的“报表中心” [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 中的 Company Sales 示例报表。|http://TestServer/TestSite/Reports/Doc/Company%20Sales.rdl|  
  
##  <a name="publishingToDocLib"></a> 从创作工具发布到 SharePoint 库  
 使用报表创作工具向库中发布报表和相关文件时，在添加文件之前会对文件进行验证。 如果通过使用 SharePoint 库的 **“上载”** 操作来上载报表和相关文件，则不进行验证检查。 直到通过管理、编辑和运行报表来访问时，您才会知道文件是否有效。  
  
> [!NOTE]  
>  为了从 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]向 SharePoint 站点发布报表，你可能需要将该 SharePoint 站点添加到 Internet Explorer 浏览器中的受信任位置列表中。  
  
### <a name="shared-data-sources"></a>共享数据源  
 从报表创作工具发布共享数据源时，应设置项目属性 `TargetDataSourceFolder`。 目标数据源文件夹必须是指向 SharePoint 库的 URL。 与在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式下不同，不能指定相对文件夹；相对路径是无效的。 如果文档库路径中不存在文件夹，则将创建一个文件夹。  
  
 将共享数据源 (.rds) 文件发布到 SharePoint 站点时，这会将数据源文件的扩展名更改为 .rsds。 无法将 .rsds 文件从 SharePoint 站点保存到本地，也无法将其导入到现有的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 项目。 文件扩展名为 .rds 和 .rsds 的共享数据源不可互换。  
  
#### <a name="shared-data-sources-from-report-designer"></a>来自报表设计器的共享数据源  
 如果从报表设计器项目发布共享数据源，可以使用指定目标库的 URL，也可以将该属性保留为空。 与在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式下不同，不能指定相对文件夹；相对路径是无效的。 如果文档库路径中不存在文件夹，则将创建一个文件夹。 如果将目标数据源文件夹保留为空，则将在目标报表文件夹中发布数据源。  
  
### <a name="file-names"></a>文件名  
 URL 中的报表项文件名必须包含文件扩展名。 文件扩展名决定文件类型。 从报表创作工具发布报表项时，会自动包含文件扩展名。 如果将报表项上载到 SharePoint 库，则必须包含文件扩展名。  
  
 如果不为上载到 SharePoint 站点的项指定文件扩展名，则会发生 `rsInvalidDataSourceReference` 错误。 文件名不可以包括 SharePoint 应用程序无法识别为有效文件名字符的字符。 不能包含以下字符: # %& *: \< >？ / { | }.  
  
## <a name="differences-between-uploading-and-publishing"></a>上载与发布之间的差异  
 使用报表设计器或报表生成器将报表和相关文件发布到库时，会在添加文件前对文件进行验证。 如果通过使用 SharePoint 库的 **“上载”** 操作来上载报表和相关文件，则不进行验证检查。 直到通过管理、编辑和运行报表来访问时，您才会知道文件是否有效。  
  
## <a name="updating-a-published-item"></a>更新已发布的项  
 将项发布或上载到 SharePoint 库后，应先从库中签出此项，然后再进行更新。 为您签出报表时，您将是唯一有权更改报表的用户。 结束操作后，将报表重新签入。  
  
 如果上载或发布报表时不先签出文档（例如上载与现有项同名的项），则报表服务器将会为您签出此文档，将更新后的报表添加为现有项的新版本，然后将此文档重新签入。  
  
## <a name="external-images-as-resources"></a>作为资源的外部图像  
 在本机模式下运行的报表服务器崇尚“资源”理念。资源指报表服务器存储和保护，但不处理的任何文件。 在本机模式下，可以是任何类型的文件。  
  
 报表服务器在 SharePoint 集成模式下运行时，资源理念的定义就会更窄。 报表服务器使用资源理念来存储引用外部图像的报表。 这适用于报表作为内部使用的快照或副本的情况。  
  
## <a name="see-also"></a>请参阅  
 [将报表发布到 SharePoint 库](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [将共享数据源发布到 SharePoint 库](../reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [“项目属性页”对话框](project-property-pages-dialog-box.md)  
  
  
