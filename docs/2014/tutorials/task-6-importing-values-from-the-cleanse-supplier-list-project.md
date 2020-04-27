---
title: 任务6：从 "清理供应商列表" 项目导入值 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f6b90a36238cd4a02e86d49125ee662f07d32882
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489093"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>任务 6：从 Cleanse Supplier List 项目导入值
  在该任务中，您将导入在清理过程中收集的数据质量知识。 有关更多详细信息，请参阅[将清理项目值导入到域](https://msdn.microsoft.com/library/hh479581.aspx)主题。 您还可以在发布更新的**供应商**知识库之前，将知识库导出到 DQS 文件中。  
  
1.  在**DQS 客户端**的主页中，单击 "**最近的知识库**" 下的 "**供应商**" 旁边的**向右箭头**，然后单击 "**域管理**"。  
  
2.  单击域列表中的 "**联系人电子邮件**"，并切换到右窗格中的 "**域值**" 选项卡。  
  
3.  单击工具栏上的 "**导入值**" 图标旁边的**向下箭头**，然后单击 "**导入项目值**"。  
  
     ![“导入项目值”工具栏按钮](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "“导入项目值”工具栏按钮")  
  
4.  在 "**导入项目值**" 对话框中，选择 "**清理供应商列表**" 项目，然后单击 **"确定"**。  
  
5.  注意，此时将导入所有电子邮件以及您在交互式清理过程中所做的两处更正内容。 滚动以查看这两处更正内容。  
  
    |Value|更正为|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  重复前面的步骤，为**Country**域导入项目值，并注意添加了一个新条目，以将**美国**更正为**美国**（包含 ""）。  
  
    |Value|更正为|  
    |-----------|----------------|  
    |United State|United States|  
  
7.  若要查看旧的域值，请清除 "**仅显示新**的" 复选框。  
  
8.  为**供应商名称**域重复导入项目值的上一步。 默认情况下，在导入后，您将只看到新值。 若要查看所有值，请清除 "**仅显示新**的" 复选框。 您已经使用了 "清理" 活动中的内容来丰富了**供应商**知识库。 知识库越强，清理结果就越好。  
  
    > [!NOTE]  
    >  无法导入复合域的值。  
  
9. 单击工具栏上的 "**导出知识库**" 图标，然后单击 "**导出知识库**"。  
  
     ![“导出知识库”菜单](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "“导出知识库”菜单")  
  
10. 导航到教程文件夹，键入 "提供**商**" 作为**文件名**，然后单击 "**保存**"。 您可以使用此 DQS 文件创建基于此文件的新知识库。  
  
11. 单击 **"确定"** 关闭 "**导出知识库-供应商**" 消息框。  
  
12. 单击 "**完成**" 完成活动。  
  
13. 单击“发布”****。  
  
14. 在消息框中单击 **"确定"** 。  
  
## <a name="next-step"></a>下一步  
 [第 3 课：匹配数据以便从供应商列表中删除重复项](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
