---
title: 第 3 课：使用报表向导设计父报表 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d2b872449bf553a00b53bcf6153befd68b6053d9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219987"
---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>第 3 课：使用报表向导设计父报表
  创建用于父报表的数据连接和数据表后，接下来要使用报表设计器中的报表向导设计父报表。 有关报表设计器的详细信息，请参阅[使用报表设计器设计报表 (SSRS)](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)。  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>使用报表向导设计父报表  
  
1.  确保在“解决方案资源管理器”中选择顶级网站。  
  
2.  右键单击该网站，然后选择“添加新项”。  
  
3.  在中**添加新项**对话框中，选择**报表向导**，输入报表文件的名称，然后单击**添加**。  
  
     随后将启动报表向导。  
  
4.  在“数据集属性”页上的“数据源”框中，选择在[第 2 课：定义用于父报表的数据连接和数据表](lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)中创建的 DataSet1。  
    随后将自动用你在上面创建的 DataTable 更新“可用数据集”框。  
  
5.  单击“下一步” 。  
  
6.  在“排列字段”页中，执行以下操作：  
  
    1.  将“ProductID”、“Name”、“ProductNumber”、“SafetyStockLevel”和“ReorderLevel”从“可用字段”拖至“值”框中。  
  
    2.  单击箭头旁边**sum （productid)**， **sum （safetystocklevel)**， **sum （reorderlevel)** 并清除**总和**所选内容。  
  
7.  单击**下一步**两次，然后单击**完成**以关闭**报表向导**。  
  
     现已创建 .rdlc 文件。 随后将在报表设计器中打开该文件。 设计图面中现在显示由您设计的 tablix。  
  
8.  保存 .rdlc 文件。  
  
## <a name="next-task"></a>下一个任务  
 您已成功地使用报表向导设计了父报表。 接下来，将创建用于子报表的数据连接和数据表。  
  
  
