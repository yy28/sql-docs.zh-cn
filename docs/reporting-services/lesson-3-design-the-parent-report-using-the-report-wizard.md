---
title: "第 3 课： 设计父报表使用报表向导 |Microsoft 文档"
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
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b491008866649087e050b04261bfde7a3ad82e92
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>第 3 课：使用报表向导设计父报表
创建用于父报表的数据连接和数据表后，接下来要使用报表设计器中的报表向导设计父报表。 有关报表设计器的详细信息，请参阅[设计报表使用报表设计器 &#40;SSRS &#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>使用报表向导设计父报表  
  
1.  请确保在中选择了顶级网站**解决方案资源管理器**。  
  
2.  右键单击网站并选择**添加新项**。  
  
3.  在**添加新项**对话框中，选择**报表向导**，输入报表文件的名称，然后选择**添加**。  
  
    随后将启动报表向导。  
  
4.  上**数据集属性**页上，在**数据源**框中，选择**DataSet1**中创建[第 2 课： 定义父报表的数据连接和数据表](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)。  
  
    **可用数据集**使用自动更新框**DataTable**你上述步骤中创建。  
  
5.  选择“下一步” 。  
  
6.  在**排列字段**页执行以下操作：  
  
    1.  拖动**ProductID**，**名称**， **ProductNumber**， **SafetyStockLevel**，和**再订购量**从**可用字段**到**值**框。  
  
    2.  选择箭头旁边**Sum(ProductID)**， **Sum(SafetyStockLevel)**， **Sum(ReorderLevel)**和清除**总和**选择。  
  
7.  选择**下一步**两次，然后选择**完成**关闭**报表向导**。  
  
    现已创建 .rdlc 文件。 随后将在报表设计器中打开该文件。 设计图面中现在显示由您设计的 tablix。  
  
8.  保存 .rdlc 文件。  
  
## <a name="next-task"></a>下一个任务  
您已成功地使用报表向导设计了父报表。 接下来，将创建用于子报表的数据连接和数据表。 请参阅 [第 4 课：定义用于子报表的数据连接和数据表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)。  
  
  
  


