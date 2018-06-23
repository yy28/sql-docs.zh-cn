---
title: 任务 3： 创建并运行用于匹配的数据质量项目 |Microsoft 文档
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
ms.topic: article
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2080aac8b429a9bc3ae21313f2163316b6cebeae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138312"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>任务 3：创建并运行数据质量项目以进行匹配
  在本任务中，您将创建匹配活动的数据质量项目并对已清理的供应商数据运行匹配过程以删除数据中的所有重复项。  
  
1.  在主页上的**DQS 客户端**，单击**新建数据质量项目**。  
  
2.  类型**删除供应商的重复项**从**项目名称**。  
  
3.  选择**供应商**从列表中的 Kb**使用知识库**字段。 您在上一课中在此知识库中创建了匹配策略。  
  
4.  选择**匹配**从**的活动列表**从右下方窗格。  
  
     ![新建数据质量项目-匹配所选](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "新建数据质量项目-匹配所选")  
  
5.  单击“下一步” 。  
  
6.  在“映射”  页中，为“数据源”  选择“Excel 文件” 。  
  
7.  单击**浏览**和选择**清理供应商 List.xls**，即清理活动的输出文件。  
  
8.  映射**供应商 Id**到源列**供应商 ID**域，**供应商名称**列**供应商名称**域和**ContactEmailAddress**列**联系人电子邮件**域。  
  
9. 单击**下一步**切换到**匹配**页。  
  
10. 单击**启动**启动匹配过程。 您应看到与上一个任务类似的结果，因为您使用了相同的输入文件来定义匹配策略。  
  
11. 在列表框中查看所有匹配的记录及其匹配分数。 结果应与您在上一个任务中看到的结果相同。 请参阅上一个任务中的步骤来分析此匹配活动的结果。  
  
12. 单击**下一步**切换到**导出**页。  
  
## <a name="next-step"></a>下一步  
 [任务 4：将匹配活动的结果导出到 Excel 文件](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)  
  
  