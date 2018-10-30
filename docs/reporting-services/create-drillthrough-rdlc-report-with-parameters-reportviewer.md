---
title: 创建带有参数的钻取 (RDLC) 报表 - ReportViewer | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 68ea91137c584959c53ee8de010dbff92106c119
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50028056"
---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>创建带有参数的钻取 (RDLC) 报表 - ReportViewer
[钻取](https://technet.microsoft.com/library/ff519554.aspx) 报表是指用户通过单击其他报表中的链接打开的报表。 钻取报表通常包含某原始汇总报表中所包含的某项的详细信息。 本教程将带你演练以下在 [本地模式报表](report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)中使用参数和查询创建钻取报表的课程。  
  
## <a name="requirements"></a>要求  
若要使用此演练，必须具有访问 **AdventureWorks2014** 示例数据库的权限。 有关如何获取 AdventureWorks2014 示例数据库的详细信息，请参阅 [AdventureWorks sample databases](https://github.com/Microsoft/sql-server-samples/releases)（AdventureWorks 示例数据库）。  
  
此演练假定你熟悉 Transaction-SQL 查询和 ADO.NET [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) 和 [DataTable](https://msdn.microsoft.com/library/system.data.datatable.aspx) 对象。  
  
使用 Visual Studio 2015 和 ASP.NET Web 应用程序创建具有 ReportViewer 控件的 ASP.NET 网页。 该控件被配置为查看您创建的报表。 对于本演练，您在 Microsoft Visual C# 中创建应用程序。  
  
## <a name="tasks"></a>“任务”  
[第 1 课：创建新网站](../reporting-services/lesson-1-create-a-new-web-site.md)  
[第 2 课：定义用于父报表的数据连接和数据表](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[第 3 课：使用报表向导设计父报表](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[第 4 课：定义用于子报表的数据连接和数据表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[第 5 课：使用报表向导设计子报表](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[第 6 课：将 ReportViewer 控件添加到应用程序](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[第 7 课：在父报表上添加钻取操作](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[第 8 课：创建数据筛选器](../reporting-services/lesson-8-create-a-data-filter.md)  
[Lesson 9: Build and Run the Application](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>另请参阅  
[Reporting Services 教程 (SSRS)](../reporting-services/reporting-services-tutorials-ssrs.md)  
[使用报表设计器设计报表 (SSRS)](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  

