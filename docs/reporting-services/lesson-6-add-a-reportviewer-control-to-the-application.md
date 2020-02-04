---
title: 第 6 课：将 ReportViewer 控件添加到应用程序 | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9b13a3653b19d4079a47941a0bb05faa2821c823
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "62512532"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>第 6 课：将 ReportViewer 控件添加到应用程序
使用报表向导设计子报表后，接下来要向网站应用程序添加 ReportViewer 控件。 如果使用 ASP.NET 报表网站，它将添加 ReportViewer 控件到 default.aspx 页。   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>向应用程序添加 ReportViewer 控件  
  
1.  在“解决方案资源管理器”中，右键单击 Default.aspx，然后单击“视图设计器”    。  
  
2.  如果 default.aspx 上已经有 ReportViewer 控件，请跳到 **第 4 步**。 否则，从“工具箱”窗口中的“AJAX 扩展”组中，将一个 ScriptManager 控件拖到设计图面上    。  
  
3.  从“报表”组中，将一个 ReportViewer 控件拖到设计图面上的 ScriptManager 控件下    。  
  
4.  通过单击 **ReportViewer** 控件右上角的箭头，打开 **ReportViewer Tasks** 窗口。  
  
5.  在“选择报表”框中，选择由你创建的父报表  。  
  
    选择某个报表后，将自动创建在该报表中使用的数据源的实例。 并将生成代码以使每个 DataTable（及其 [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) 容器）实例化。 向设计图面添加 [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx) 控件，对应于报表中使用的每个数据源。 此数据源控件为自动配置。  
  
6.  在“生成”菜单上，单击“生成网站”。  
  
    该报表随即进行编译，并在“错误列表”区域中显示任何错误（例如报表表达式中的语法错误）  。 单击 Visual Studio 窗口底部的“错误列表”以显示“错误列表”区域   。  
  
## <a name="next-task"></a>下一个任务  
您已成功地将 ReportViewer 控件添加到网站应用程序。 接下来，将在父报表上添加钻取操作。 请参阅 [第 7 课：在父报表上添加钻取操作](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)。  
  

