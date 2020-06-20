---
title: 任务5：将清理结果导出到 Excel 文件 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 44c926d2429a0d9842e9e9202568f73f72c89d9a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064744"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>任务 5：将清理结果导出到 Excel 文件
  在本任务中，您将清理活动的结果导出到 Excel 文件。 有关更多详细信息，请参阅[导出阶段](https://msdn.microsoft.com/library/hh213061.aspx#Export)主题。  
  
1.  在右侧窗格中，选择 " **Excel** " 作为**目标类型**。  
  
2.  单击 "**浏览**"，将输出文件名指定为**清理供应商 List.xls**，然后单击 "**打开**"。  
  
3.  仅选择 "要导出的**数据**" 作为**输出**格式，以便只导出清理的数据。 第二个选项 "**数据和清理信息**" 允许您导出清理活动详细信息以及清理数据。 使用 "**标准化格式**" 选项，您可以将域中定义的任何输出格式应用于该域的值。 在本教程中，您尚未在任何域上定义输出格式。  
  
     ![“导出清理结果”页](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "“导出清理结果”页")  
  
4.  单击 "**导出**" 以导出数据。 不要单击 "**完成**"。  
  
5.  单击 "**导出**" 对话框中的 "**关闭**"。  
  
6.  单击 "**完成**" 完成活动。 如果您在单击 "**完成**" 之前忘了导出结果，请在 " **DQS 客户端**" 的主页中单击 "**打开数据质量项目**"，从项目列表中选择 "**清理供应商列表**"，然后单击屏幕底部的 "**下一步**" 以再次转到清理过程的**导出**阶段。 还可以通过单击 "**后退**" 按钮切换到 "**管理和查看结果**" 选项卡。  
  
7.  打开**清理供应商 List.xls**并执行以下操作：  
  
    1.  通过在工作表中搜索 adventure-work.com，确保不存在以 adventure-work.com （不含字符 '）结尾的电子邮件地址。  
  
    2.  请注意，"**国家/地区**" 列中没有任何**USA**值。  
  
    3.  搜索洛杉矶 **，并看到**"**状态**" 设置为 " **CA**"。  
  
    4.  确认没有术语 " **Co**"、" **Corp**" 和 " **inc.**"。  
  
    5.  从电子表格中删除**地址验证**列，并保存该 excel 文件。 此额外列对应于“地址验证”复合域。  
  
## <a name="next-step"></a>下一步  
 [任务 6：从 Cleanse Supplier List 项目导入值](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
