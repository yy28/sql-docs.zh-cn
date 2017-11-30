---
title: "第 5 课：使用报表向导设计子报表 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: "8"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b84722749ad94251c057a43858e2da98b37d2adb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>第 5 课：使用报表向导设计子报表
创建用于子报表的数据连接和数据表后，接下来要使用报表设计器中的报表向导设计子报表。 有关报表设计器的详细信息，请参阅[使用报表设计器设计报表 (SSRS)](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)。  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>使用报表向导设计子报表  
  
1.  确保在“解决方案资源管理器”中选择顶级网站。  
  
2.  右键单击该网站，然后选择“添加新项”。  
  
3.  在“添加新项”对话框中，单击“报表向导”，输入报表文件的名称，然后选择“添加”。  
  
    随后将启动报表向导。  
  
4.  在“数据集属性”页的“数据源”框中，选择“DataSet2”。  
  
    随后将自动使用创建的 DataTable 更新“可用数据集”框。  
  
5.  选择“下一步” 。  
  
6.  在“排列字段”页中，执行以下操作：  
  
    1.  将 ProductID、PurchaseOrderID、PurchaseOrderDetailID、OrderQty、ReceivedQty、RejectedQty 和 StockedQty 从“可用字段”拖到“值”框中。  
  
    2.  选择 **Sum(ProductID)**、 **Sum(PurchaseOrderID)**、 **Sum(PurchaseOrderDetailID)**、 **Sum(OrderQty)**、 **Sum(ReceivedQty)**、 **Sum(RejectedQty)**和 **Sum(StockedQty)** 旁的箭头，然后取消选择 **Sum** 。  
  
7.  选择“下一步”两次，然后选择“完成”以关闭“报表向导”。  
  
    现已创建 .rdlc 文件。 随后将在报表设计器中打开该文件。 设计图面中现在显示由您设计的 tablix。  
  
8.  打开 .rdlc 文件后，通过执行以下操作添加参数：  
  
    1.  在“报表数据”窗格中右键单击“参数”，然后选择“添加参数”。  
  
    2.  在“名称”框中输入“productid”。  
  
    3.  确认在“数据类型”列表框中选择了“整数”。  
  
    4.  单击 **“确定”**。  
  
9. 保存 .rdlc 文件。  
  
## <a name="next-task"></a>下一个任务  
您已成功地使用报表向导设计了子报表。 接下来，将向网站应用程序添加 ReportViewer 控件。 请参阅 [第 6 课：将 ReportViewer 控件添加到应用程序](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)。  
  
  
  

