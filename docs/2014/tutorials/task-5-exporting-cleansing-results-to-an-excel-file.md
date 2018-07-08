---
title: 任务 5： 将导出清理结果保存到 Excel 文件 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3cc3e51ee8b07ad017e6bf33150ec83e30ec4ff8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155528"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>任务 5：将清理结果导出到 Excel 文件
  在本任务中，您将清理活动的结果导出到 Excel 文件。 请参阅[导出阶段](http://msdn.microsoft.com/library/hh213061.aspx#Export)主题的更多详细信息。  
  
1.  在右窗格中，选择**Excel**有关**目标类型**。  
  
2.  单击**浏览**，指定输出文件的名称作为**Cleansed Supplier List.xls**，然后单击**打开**。  
  
3.  选择**Data Only**有关**输出**格式导出已清理的数据。 第二个选项，**数据和清理信息**，你可以将导出清理活动详细信息，以及已清理的数据。 **标准化格式**选项可将应用到该域的值在域定义的任何输出格式。 在本教程中，您尚未在任何域上定义输出格式。  
  
     ![导出清理结果页面](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "导出清理结果页")  
  
4.  单击**导出**导出的数据。 不要单击**完成**尚未。  
  
5.  单击**关闭**上**导出**对话框。  
  
6.  单击**完成**以完成活动。 如果您忘记了导出结果，再单击**完成**，单击**打开数据质量项目**中的主页**DQS 客户端**，选择**清理供应商列表**从列表中的项目，然后单击**下一步**屏幕中获取到底部**导出**阶段的试清理过程。 此外可以切换到**管理和查看结果**通过单击选项卡**回**按钮。  
  
7.  打开**Cleansed Supplier List.xls**并执行以下操作：  
  
    1.  通过在工作表中搜索 adventure-work.com，确保没有电子邮件地址以 adventure-work.com 结尾（没有字符“s”）。  
  
    2.  查看任何**USA**中的值**国家/地区**列。  
  
    3.  搜索**Los Angeles**看到**状态**设置为**CA**。  
  
    4.  确认没有术语**Co.**， **Corp.**，并**Inc.**。  
  
    5.  删除**地址验证**列从电子表格并保存 excel 文件。 此额外列对应于“地址验证”复合域。  
  
## <a name="next-step"></a>下一步  
 [任务 6：从 Cleanse Supplier List 项目导入值](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
