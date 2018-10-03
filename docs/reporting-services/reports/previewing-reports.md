---
title: 预览报表 | Microsoft Docs
ms.date: 05/05/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], previewing reports
- previewing reports [Reporting Services]
- printing previews
- test servers [Reporting Services]
ms.assetid: 85117f6c-828e-45c9-810f-e700d9bfba67
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec8ba62b63324bb8aceeef976a482325af9248d0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785435"
---
# <a name="previewing-reports"></a>预览报表
  在设计     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表时，在将报表发布到生产环境中之前可能需要查看该报表。 可使用多种方法查看该报表：在报表设计器中切换到预览模式、使用报表设计器中的预览窗口以及在测试环境中将报表发布到报表服务器。  
  
> [!NOTE]  
>  在预览报表时，报表数据将缓存到本地计算机上的文件中。 使用相同的查询、参数和凭据再次预览同一报表时，报表设计器将检索缓存副本，而不是重新运行查询。 数据文件将在报表定义文件所在的同一目录中另存为 \<reportname>.rdl.data。 关闭报表设计器时，不会删除该文件。  
  
## <a name="preview-mode"></a>预览模式  
 单击 ![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png "ssrs_ssdt_preview") 可以在报表设计器中预览报表。 这将在本地运行报表，使用的报表处理功能和呈现功能与报表服务器所提供的功能相同。 所显示的报表是一个交互式的图像；您可以选择参数、单击链接、查看文档结构图以及展开和折叠报表的隐藏区域。 您还可以使用所安装的任意一种呈现格式将报表导出。  
  
## <a name="standalone-preview"></a>独立预览  
 预览报表的另一种方法是使用调试配置运行报表项目，例如，调试您编写的自定义程序集。 将在默认浏览器中打开报表。 运行项目的方法有以下三种：  
  
-   通过在“调试”菜单上单击“启动调试”。  
  
-   通过在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 标准工具栏 ![ssrs_ssdt_startdebug](../../reporting-services/reports/media/ssrs-ssdt-startdebug.png "ssrs_ssdt_startdebug") 上单击“启动”按钮。  
  
-   按 **F5**。  
  
 如果使用生成报表但不部署该报表的项目配置，则将在单独的预览窗口中打开在当前配置的 **StartItem** 属性中指定的报表。 预览窗口显示报表的方式与预览模式相同，并具有相同功能。  
  
> [!NOTE]  
>  在调试报表之前，必须设置开始项。 例如，如果运行调试模式，浏览器将打开主报表服务器页，而不是预览模式下的报表。 若要设置启动项，请在解决方案资源管理器中右键单击报表项目，再单击“属性”，然后在 StartItem 中选择要显示的报表的名称。  
  
 若要预览项目开始项之外的特定报表，请选择生成报表但不部署该报表的配置（例如，DebugLocal 配置），右键单击报表，再单击 **“运行”**。 必须选择不部署报表的配置；否则，报表将发布到报表服务器，而不是显示在本地预览窗口中。  
  
## <a name="publishing-to-a-test-server"></a>发布到测试服务器  
 也可以通过将报表发布到测试服务器来测试、浏览和预览报表。 将报表发布到测试服务器与发布到生产服务器是相同的。 有关发布报表的信息，请参阅 [将报表发布到报表服务器](../../reporting-services/reports/publishing-reports-to-a-report-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)   
 [发布报表](http://msdn.microsoft.com/library/ef5a514e-e818-4041-a8b0-15835f9a046b)   
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
