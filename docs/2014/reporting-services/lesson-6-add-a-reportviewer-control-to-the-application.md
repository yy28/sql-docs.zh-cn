---
title: 第 6 课：将 ReportViewer 控件添加到应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dfce5e2bdf71dfb58481fedf05794d3603285449
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108421"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>第 6 课：向应用程序添加 ReportViewer 控件
  使用报表向导设计子报表后，接下来要向网站应用程序添加 ReportViewer 控件。  
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>向应用程序添加 ReportViewer 控件  
  
1.  在“解决方案资源管理器”中，右键单击 Default.aspx，然后单击“视图设计器”。  
  
2.  从**AJAX Extensions**组中**工具箱**窗口中，拖动**ScriptManager**至设计图面上的控件。  
  
3.  从“报表”组中，将一个 ReportViewer 控件拖到设计图面上的 ScriptManager 控件下。  
  
4.  通过单击 **ReportViewer** 控件右上角的箭头，打开 **ReportViewer Tasks** 窗口。  
  
5.  在中**选择报表**框中，选择你创建的父报表。  
  
     选择某个报表后，将自动创建在该报表中使用的数据源的实例。 并将生成代码以使每个 DataTable（及其 [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) 容器）实例化。 向设计图面添加 [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource\(v=vs.100\).aspx) 控件，对应于报表中使用的每个数据源。 此数据源控件为自动配置。  
  
     如果您使用 Microsoft Visual Studio 2012，请确保如果中列出的完全限定的名称，与为项目命名空间，使用完全限定的 DataSet1 绑定 ObjectDataSource 控件**选择业务对象**下拉列表框 (例如 Projectnamespace.DataSet1TableAdapters.ProductTableAdapter)。 通过右键单击 ObjectDataSource，然后单击访问该列表框**配置数据源**。  
  
6.  在“生成”菜单上，单击“生成网站”。  
  
     该报表随即进行编译，并在“错误列表”区域中显示任何错误（例如报表表达式中的语法错误）。 单击 Visual Studio 窗口底部的“错误列表”以显示“错误列表”区域。  
  
## <a name="next-task"></a>下一个任务  
 您已成功地将 ReportViewer 控件添加到网站应用程序。 接下来，将在父报表上添加钻取操作。  
  
  
