---
title: 任务 5：导出清理结果保存到 Excel 文件 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: aab1eff896ba602f118606b8f80894260e26f7ec
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028918"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>任务 5：将清理结果导出到 Excel 文件
  在本任务中，您将清理活动的结果导出到 Excel 文件。 请参阅[导出阶段](https://msdn.microsoft.com/library/hh213061.aspx#Export)主题的更多详细信息。  
  
1.  在右窗格中，选择**Excel**有关**目标类型**。  
  
2.  单击**浏览**，指定输出文件的名称作为**Cleansed Supplier List.xls**，然后单击**打开**。  
  
3.  选择**Data Only**有关**输出**格式导出已清理的数据。 第二个选项，**数据和清理信息**，你可以将导出清理活动详细信息，以及已清理的数据。 **标准化格式**选项可将应用到该域的值在域定义的任何输出格式。 在本教程中，您尚未在任何域上定义输出格式。  
  
     ![导出清理结果页面](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "导出清理结果页")  
  
4.  单击**导出**导出的数据。 不要单击**完成**尚未。  
  
5.  单击**关闭**上**导出**对话框。  
  
6.  单击**完成**以完成活动。 如果您忘记了导出结果，再单击**完成**，单击**打开数据质量项目**中的主页**DQS 客户端**，选择**清理供应商列表**从列表中的项目，然后单击**下一步**屏幕中获取到底部**导出**阶段的试清理过程。 此外可以切换到**管理和查看结果**通过单击选项卡**回**按钮。  
  
7.  打开**Cleansed Supplier List.xls**并执行以下操作：  
  
    1.  确保没有电子邮件地址以 adventure-work.com 结尾 (没有字符的) 通过搜索 adventure-work.com 工作表中。  
  
    2.  查看任何**USA**中的值**国家/地区**列。  
  
    3.  搜索**Los Angeles**看到**状态**设置为**CA**。  
  
    4.  确认没有术语**Co.**， **Corp.**，并**Inc.**。  
  
    5.  删除**地址验证**列从电子表格并保存 excel 文件。 此额外列对应于“地址验证”复合域。  
  
## <a name="next-step"></a>下一步  
 [任务 6:导入值从 Cleanse Supplier List 项目](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
