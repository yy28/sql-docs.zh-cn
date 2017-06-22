---
title: "第 1 课： 创建报表服务器项目 (Reporting Services) |Microsoft 文档"
ms.custom: 
ms.date: 11/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
caps.latest.revision: 57
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bead48dd2f32047b2782a54204bf06a145a7d71d
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>第 1 课：创建报表服务器项目 (Reporting Services)

 > 与以前版本的 SQL Server 相关的内容，请参阅[第 1 课： 创建报表服务器项目 (Reporting Services)](https://msdn.microsoft.com/en-US/library/ms167559(SQL.120).aspx)。

在本课程中，将在 Visual Studio 内的 *中创建报表服务器项目**和报表定义 (.rdl)*[!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)] 文件。 

若要使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]创建报表，首先需要一个报表服务器项目，可用于保存报表定义 (.rdl) 文件和报表所需的其他资源文件。 

在接下来的课程中，定义报表的数据源、定义数据集并定义报表布局。 运行报表时，将检索数据并将其与布局相结合，然后呈现在屏幕上。 可以从屏幕执行导出、打印或保存操作。  
  
  
  
## <a name="to-create-a-report-server-project"></a>创建报表服务器项目  
  
1.  打开 [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)]。  
  
2.  在“文件”菜单上，转到“新建” > “项目”。  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
3.  在“已安装” > “模板” > “商业智能”下，单击 **Reporting Services**。

    ![ssrs-ssdt-01-new-rs-project](../reporting-services/media/ssrs-ssdt-01-new-rs-project.png)

5. 单击“报表服务器项目”![ssrs_ssdt_report_server_project](../reporting-services/media/ssrs-ssdt-report-server-project.png)。 

   >**请注意**： 如果看不到**Business Intelligence**或**报表服务器项目**选项，你需要使用商业智能模板更新 SSDT。 请参阅 [下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)  
  
5.  在“名称” 中，键入 **Tutorial**。  

    默认将它创建在新目录中的 Visual Studio 2015\Projects 文件夹中。
    
    ![ssrs-ssdt-01-solution-location](../reporting-services/media/ssrs-ssdt-01-solution-location.png)
  
6.  单击 **“确定”** 以创建项目。  
  
    Tutorial 项目显示在右侧的“解决方案资源管理器”窗格中。  
  
## <a name="to-create-a-new-report-definition-file"></a>创建新的报表定义文件  
  
1.  在**解决方案资源管理器**窗格中，右键单击**报表** > **添加** > **新项**。 

    >**提示**：如果看不到“解决方案资源管理器”窗格，请单击“视图”菜单上的“解决方案资源管理器”。 

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)
  
2.  在“添加新项”窗口中，单击“报表”![ssrs_ssdt_report](../reporting-services/media/ssrs-ssdt-report.png)。  
  
3.  在“名称”中，键入 **Sales Orders.rdl**，再单击“添加”。  
  
    此时报表设计器将打开，并在“设计”视图中显示新的 .rdl 文件。  
    
    ![ssrs-ssdt-01-new-report-designer](../reporting-services/media/ssrs-ssdt-01-new-report-designer.png)
  
     报表设计器是在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中运行的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]组件。 它包含两个视图：“设计”  和“预览” 。 单击各个选项卡可更改视图。  
  
    在“报表数据”  窗格中定义数据。 在“设计”  视图中定义报表布局。 可以在“预览”  视图中运行报表并查看其外观。  
  
## <a name="next-lesson"></a>下一课  
您已经成功创建了名为“Tutorial”的报表项目，并向该报表项目添加了报表定义 (.rdl) 文件。 接下来，您将指定要用于报表的数据源。 请参阅[第 2 课：指定连接信息 (Reporting Services)](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
[创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  


