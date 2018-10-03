---
title: 预览报表 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], previewing reports
- previewing reports [Reporting Services]
- printing previews
- test servers [Reporting Services]
ms.assetid: 85117f6c-828e-45c9-810f-e700d9bfba67
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b839c8124e880cfc1837cc17a8e45e30c50bab31
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105807"
---
# <a name="previewing-reports"></a>预览报表
  在设计报表时，在将报表发布到生产环境中之前可能需要查看该报表。 可使用多种方法查看该报表：在报表设计器中切换到预览模式、使用报表设计器中的预览窗口以及在测试环境中将报表发布到报表服务器。  
  
> [!NOTE]  
>  在预览报表时，报表数据将缓存到本地计算机上的文件中。 使用相同的查询、参数和凭据再次预览同一报表时，报表设计器将检索缓存副本，而不是重新运行查询。 数据文件将在报表定义文件所在的同一目录中另存为 \<reportname>.rdl.data。 关闭报表设计器时，不会删除该文件。  
  
## <a name="preview-mode"></a>预览模式  
 可以通过单击预览报表设计器中的报表**预览版**。 这将在本地运行报表，使用的报表处理功能和呈现功能与报表服务器所提供的功能相同。 所显示的报表是一个交互式的图像；您可以选择参数、单击链接、查看文档结构图以及展开和折叠报表的隐藏区域。 您还可以使用所安装的任意一种呈现格式将报表导出。  
  
## <a name="standalone-preview"></a>独立预览  
 预览报表的另一种方法是使用调试配置运行报表项目，例如，调试您编写的自定义程序集。 运行项目的方法有以下三种：  
  
-   通过单击**启动**上**调试**菜单。  
  
-   通过单击**启动**按钮[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]标准工具栏。  
  
-   按 F5。  
  
 如果您使用项目配置，生成报表但不部署该报表中指定，`StartItem`当前配置的属性将在单独的预览窗口中打开。 预览窗口显示报表的方式与预览模式相同，并具有相同功能。  
  
> [!NOTE]  
>  在调试报表之前，必须设置开始项。 若要设置启动项，请在解决方案资源管理器中右键单击报表项目，单击**属性**，然后在`StartItem`，选择要显示的报表的名称。  
  
 若要预览项目开始项之外的特定报表，请选择生成报表但不部署该报表的配置（例如，DebugLocal 配置），右键单击报表，再单击 **“运行”**。 必须选择不部署报表的配置；否则，报表将发布到报表服务器，而不是显示在本地预览窗口中。  
  
## <a name="print-preview"></a>打印预览  
 首次在预览模式下或在预览窗口中查看报表时，报表的视图类似于 HTML 呈现扩展插件所生成的报表。 虽然预览并非 HTML 格式，但报表的布局和分页与 HTML 格式的输出结果类似。  
  
 可通过切换到打印预览模式，查看报表的打印效果。 单击预览工具栏上的 **“打印预览”** 按钮。 所显示的报表就如同打印在纸张上一样。 此视图与图像呈现扩展插件和 PDF 呈现扩展插件所生成的输出类似。 虽然打印预览并非图像或 PDF 文件，但报表的布局和分页与这些格式的输出类似。  
  
## <a name="publishing-to-a-test-server"></a>发布到测试服务器  
 也可以通过将报表发布到测试服务器来对其进行测试。 将报表发布到测试服务器与发布到生产服务器是相同的。 有关发布报表的信息，请参阅 [将报表发布到报表服务器](publishing-reports-to-a-report-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [打印报表（报表生成器和 SSRS）](../report-builder/print-reports-report-builder-and-ssrs.md)   
 [打印报表（报表生成器和 SSRS）](../report-builder/print-a-report-report-builder-and-ssrs.md)   
 [发布报表](../publish-reports.md)   
 [将自定义程序集用于报表](../custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
