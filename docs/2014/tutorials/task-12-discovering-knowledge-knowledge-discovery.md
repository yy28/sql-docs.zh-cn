---
title: 任务 12：发现知识 （知识发现） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6dd54475ee63b2f6ef5e1b56b94c11aafd5996ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484685"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>任务 12：发现知识（知识发现）
  在本任务中，您将执行**知识发现**上的活动**Supplier ID**并**Supplier Name**域。 在此方案中，知识发现过程主要导入这两个域的值。  
  
 在本教程中，您是从头开始构建知识库的。 还可以通过执行知识发现活动来创建知识库。 当您单击**创建的知识库**主页上，在 DQS 客户端将您带入一个页面与**域管理**选择活动的活动。 您可以更改**活动**到**知识发现**，然后在下一步页可以创建域知识发现过程的一部分。 请参阅[执行知识发现](https://msdn.microsoft.com/library/hh510398.aspx)的更多详细信息。  
  
1.  在 DQS 客户端的主页中**最近的知识库**部分中，单击**右箭头**旁边**供应商**知识库和单击**知识发现**。 或者，你可以单击**打开知识库**，选择**供应商**从**知识库列表**，选择**知识发现**作为**活动**然后单击**下一步**。  
  
     ![在主菜单中的知识发现页](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "在主菜单中的知识发现页")  
  
2.  选择**Excel 文件**有关**数据源**。  
  
3.  单击**浏览**，导航并选择**Suppliers.xls**，然后单击**打开**。  
  
4.  选择**Suppliers for Discovery**有关**工作表**。  
  
5.  在中**映射**部分中，将**SupplierID**从列**Excel**文件为**Supplier ID**域和**供应商名称**列添加到**Supplier Name**使用的域**下拉列表**。 Excel 文件具有的示例数据**供应商 ID**并**Supplier Name**域。 在发现过程中，您可以选择要为其发现值的域。 您可以在此页上创建域，然后将源列映射到这些域。 在知识发现活动中创建域的情况并不少见，而不是在域管理活动期间创建域。  
  
     ![映射页的发现进程](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "映射页的发现过程")  
  
6.  单击**下一步**若要切换到**Discover**页。  
  
7.  上**Discover**页上，单击**启动**若要开始发现过程。 对列执行发现**SupplierID**并**Supplier Name**中**Suppliers.xls**文件。 **供应商 ID**并**Supplier Name**域应填充了发现过程中获得的知识。  
  
     ![发现页的发现进程](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "发现页的发现过程")  
  
8.  在分析完成后，请查看**源统计信息**中**Profiler 选项卡**页的底部。 请注意，10 个新记录以及总共 20 个值 (**SupplierID**并**Supplier Name**中的值**Excel 工作表**) 发现。 我们还看到多少个值是新的、唯一的、新并且是唯一的以及有效的。 在右侧的列表框中，您可以看到发现过程中涉及的每个域的详细信息。 如果您将鼠标悬停在“完整性”列的状态栏上，您可以看到源列中是否有任何缺失值。  
  
     ![知识发现结果](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "知识发现结果")  
  
9. 单击**下一步**若要切换到**管理域值**页。  
  
10. 在中**管理域值**页上，单击**Supplier Name**从域列表的域。  
  
11. 在右窗格中，右键单击**Lazy Country Storex** （注意，x 结尾），然后选择**Lazy Country Store**。 DQS 建议在对域运行拼写检查程序后进行此更改。 默认情况下，在您创建的域上启用拼写检查程序。  
  
     ![正确供应商名称-惰性国家/地区应用商店](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "正确供应商名称-惰性国家/地区应用商店")  
  
12. 在域值列表中，确认该值**Lazy Country Storex**设置为错误 (红色**X**标记) 与**Lazy Country Store**作为更正以及**Lazy Country Store**也添加为有效的值。  
  
     ![域值和更正为值](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "域值和更正为值")  
  
13. 单击 **“完成”** 。  
  
14. 上**SQL Server Data Quality Services**对话框中，单击**发布**。  
  
15. 单击**确定**成功消息框上。  
  
     您已经完成本教程的第一个课程。  
  
## <a name="next-step"></a>下一步  
 [第 2 课：使用 Suppliers 知识库清理供应商数据](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
