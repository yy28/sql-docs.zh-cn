---
title: 预览报表
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 21928cd6637815000983e8a0fe05aa4e77d1c216
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67412974"
---
# <a name="preview-reports-in-sql-server-reporting-services-ssrs"></a>预览 SQL Server Reporting Services (SSRS) 中的报表

  在设计报表时，在将报表发布到生产环境中之前可能需要查看该报表。 可使用多种方法查看该报表：在报表设计器中切换到预览模式、使用报表设计器中的预览窗口以及在测试环境中将报表发布到报表服务器。  
  
> [!NOTE]  
> 在预览报表时，报表数据将缓存到本地计算机上的文件中。 使用相同的查询、参数和凭据再次预览同一报表时，报表设计器将检索缓存副本，而不是重新运行查询。 数据文件在报表定义文件所在的同一目录中另存为* \<reportname>*。 关闭报表设计器时，不会删除该文件。  
  
## <a name="preview-mode"></a>预览模式

 可以通过单击 "**预览**" 在报表设计器中预览报表。 这将在本地运行报表，使用的报表处理功能和呈现功能与报表服务器所提供的功能相同。 所显示的报表是一个交互式的图像；您可以选择参数、单击链接、查看文档结构图以及展开和折叠报表的隐藏区域。 您还可以使用所安装的任意一种呈现格式将报表导出。  
  
## <a name="standalone-preview"></a>独立预览

 预览报表的另一种方法是使用调试配置运行报表项目，例如，调试您编写的自定义程序集。 运行项目的方法有以下三种：  
  
- 单击 "**调试**" 菜单上的 "**启动**"。  
  
- 单击 " [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]标准" 工具栏上的 "**开始**" 按钮。  
  
- 按 F5。  
  
 如果使用生成报表但不部署该报表的项目配置，则将在单独的预览窗口中打开在当前配置的 `StartItem` 属性中指定的报表。 预览窗口显示报表的方式与预览模式相同，并具有相同功能。  
  
> [!NOTE]  
> 在调试报表之前，必须设置开始项。 若要设置启动项，请在解决方案资源管理器中右键单击报表项目，再单击 "**属性**"，然后`StartItem`在中，选择要显示的报表的名称。  
  
 若要预览项目开始项之外的特定报表，请选择生成报表但不部署该报表的配置（例如，DebugLocal 配置），右键单击报表，再单击 **“运行”**。 必须选择不部署报表的配置；否则，报表将发布到报表服务器，而不是显示在本地预览窗口中。  
  
## <a name="print-preview"></a>打印预览

 首次在预览模式下或在预览窗口中查看报表时，报表的视图类似于 HTML 呈现扩展插件所生成的报表。 虽然预览并非 HTML 格式，但报表的布局和分页与 HTML 格式的输出结果类似。  
  
 可通过切换到打印预览模式，查看报表的打印效果。 单击预览工具栏上的 **“打印预览”** 按钮。 所显示的报表就如同打印在纸张上一样。 此视图与图像呈现扩展插件和 PDF 呈现扩展插件所生成的输出类似。 虽然打印预览并非图像或 PDF 文件，但报表的布局和分页与这些格式的输出类似。  
  
## <a name="publish-to-a-test-server"></a>发布到测试服务器

 也可以通过将报表发布到测试服务器来对其进行测试。 将报表发布到测试服务器与发布到生产服务器是相同的。 有关发布报表的信息，请参阅 [将报表发布到报表服务器](publishing-reports-to-a-report-server.md)。  
  
## <a name="next-steps"></a>后续步骤

 - [打印报表（报表生成器和 SSRS）](../report-builder/print-reports-report-builder-and-ssrs.md)
 - [打印报表（报表生成器和 SSRS）](../report-builder/print-a-report-report-builder-and-ssrs.md)
 - [发布报表](../publish-reports.md)
 - [将自定义程序集用于报表](../custom-assemblies/using-custom-assemblies-with-reports.md)