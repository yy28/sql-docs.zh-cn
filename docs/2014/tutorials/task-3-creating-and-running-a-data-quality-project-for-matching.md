---
title: 任务3：创建并运行数据质量项目以进行匹配 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c6953214bd5e5353643cb16b75ed51ac18783256
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171766"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>任务 3：创建并运行数据质量项目以进行匹配
  在本任务中，您将创建匹配活动的数据质量项目并对已清理的供应商数据运行匹配过程以删除数据中的所有重复项。

1.  在**DQS 客户端**的主页上，单击 "**新建数据质量项目**"。

2.  键入 "删除**项目名称中的****供应商重复项**"。

3.  从 "**使用知识库**" 字段的 kb 列表中选择 "**供应商**"。 您在上一课中在此知识库中创建了匹配策略。

4.  从右下方窗格的**活动列表**中选择 "**匹配**"。

     ![新建数据质量项目 - 已选择匹配](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "新建数据质量项目 - 已选择匹配")

5.  单击“下一步”。 

6.  在“映射” **** 页中，为“数据源” **** 选择“Excel 文件” ****。

7.  单击 "**浏览**" 并选择 "**清理供应商列表 .xls**"，这是清理活动的输出文件。

8.  将**供应商的源列**映射到供应商**ID**域、**供应商名称**列到**供应商名称**域，并将**ContactEmailAddress**列映射到**联系人电子邮件**域。

9. 单击 "**下一步**" 切换到 "**匹配**" 页。

10. 单击 "**启动**" 以启动匹配进程。 您应看到与上一个任务类似的结果，因为您使用了相同的输入文件来定义匹配策略。

11. 在列表框中查看所有匹配的记录及其匹配分数。 结果应与您在上一个任务中看到的结果相同。 请参阅上一个任务中的步骤来分析此匹配活动的结果。

12. 单击 "**下一步**" 切换到 "**导出**" 页。

## <a name="next-step"></a>下一步
 [任务 4：将匹配活动的结果导出到 Excel 文件](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)


