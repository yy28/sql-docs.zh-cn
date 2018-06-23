---
title: 创建带有使用 ReportViewer （SSRS 教程） 的参数的钻取 (RDLC) 报表 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 2124efb2b773f76b6d117d9163b159affb79ffac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125807"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>使用 ReportViewer 创建带有参数的钻取 (RDLC) 报表（SSRS 教程）
  [钻取](http://technet.microsoft.com/library/ff519554.aspx)报表是指用户通过单击其他报表中的链接打开的报表。 钻取报表通常包含某原始汇总报表中所包含的某项的详细信息。 本教程将带你演练以下在 [本地模式报表](http://msdn.microsoft.com/library/ff487969.aspx)中使用参数和查询创建钻取报表的课程。  
  
## <a name="requirements"></a>要求  
 若要使用本演练，你必须有权**AdventureWorks2008**示例数据库。 在本演练中所使用的查询还会使用**AdventureWorks2012**数据库。 有关如何获取详细信息**AdventureWorks2008**示例数据库，请参阅[演练： 安装 AdventureWorks 数据库](http://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)for Microsoft Visual Studio 2010。  
  
 本演练假定你已经熟悉 TRANSACTION-SQL 查询以及 ADO.NET[数据集](http://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx)和[DataTable](http://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx)对象。  
  
 使用 Visual Studio 2010 或 Visual Studio 2012 和 ASP.NET 网站模板创建具有 ReportViewer 控件的 ASP.NET 网页。 该控件被配置为查看您创建的报表。 对于本演练，您在 Microsoft Visual C# 中创建应用程序。  
  
## <a name="tasks"></a>“任务”  
 [第 1 课： 创建新的网站](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [第 2 课： 定义父报表的数据连接和数据表](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [第 3 课： 设计父报表使用报表向导](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [第 4 课： 定义子报表的数据连接和数据表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [第 5 课： 设计子报表使用报表向导](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [第 6 课： 将 ReportViewer 控件添加到应用程序](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [在父报表上的第 7 课： 添加钻取操作](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [第 8 课： 创建数据筛选器](../reporting-services/lesson-8-create-a-data-filter.md)   
 [第 9 课：生成并运行应用程序](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 教程 (SSRS)](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [使用报表设计器设计报表 (SSRS)](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  