---
title: "第 5 课： 设计子报表使用报表向导 |Microsoft 文档"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 285ade0eaf63fee0733fcfcb9e8f627e8c666a6b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>第 5 课：使用报表向导设计子报表
创建用于子报表的数据连接和数据表后，接下来要使用报表设计器中的报表向导设计子报表。 有关报表设计器的详细信息，请参阅[设计报表使用报表设计器 &#40;SSRS &#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>使用报表向导设计子报表  
  
1.  请确保在中选择了顶级网站**解决方案资源管理器**。  
  
2.  右键单击网站并选择**添加新项**。  
  
3.  在**添加新项**对话框中，单击**报表向导**，输入报表文件的名称，然后选择**添加**。  
  
    随后将启动报表向导。  
  
4.  在**数据集属性**页上，在**数据源**框中，选择**DataSet2**。  
  
    **可用数据集**使用您创建的 DataTable 自动更新框。  
  
5.  选择“下一步” 。  
  
6.  在**排列字段**页执行以下操作：  
  
    1.  拖动**ProductID**， **PurchaseOrderID**， **PurchaseOrderDetailID**， **OrderQty**， **ReceivedQty**， **RejectedQty**，和**StockedQty**从**可用字段**到**值**框。  
  
    2.  选择 **Sum(ProductID)**、 **Sum(PurchaseOrderID)**、 **Sum(PurchaseOrderDetailID)**、 **Sum(OrderQty)**、 **Sum(ReceivedQty)**、 **Sum(RejectedQty)**和 **Sum(StockedQty)** 旁的箭头，然后取消选择 **Sum** 。  
  
7.  选择**下一步**两次，然后选择**完成**关闭**报表向导**。  
  
    现已创建 .rdlc 文件。 随后将在报表设计器中打开该文件。 设计图面中现在显示由您设计的 tablix。  
  
8.  打开 .rdlc 文件后，通过执行以下操作添加参数：  
  
    1.  右键单击**参数**中**报表数据**窗格中，，然后选择**添加参数**。  
  
    2.  输入**productid**中**名称**框。  
  
    3.  确认**整数**中选择**数据类型**列表框。  
  
    4.  单击 **“确定”**。  
  
9. 保存 .rdlc 文件。  
  
## <a name="next-task"></a>下一个任务  
您已成功地使用报表向导设计了子报表。 接下来，将向网站应用程序添加 ReportViewer 控件。 请参阅 [第 6 课：将 ReportViewer 控件添加到应用程序](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)。  
  
  
  


