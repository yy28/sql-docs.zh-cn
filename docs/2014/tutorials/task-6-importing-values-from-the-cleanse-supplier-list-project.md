---
title: 任务 6:导入值从 Cleanse Supplier List 项目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0780636d3bcaecfe0519192bd450bb538d78bbf9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866767"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>任务 6:导入值从 Cleanse Supplier List 项目
  在该任务中，您将导入在清理过程中收集的数据质量知识。 请参阅[清理项目值导入到域](https://msdn.microsoft.com/library/hh479581.aspx)主题的更多详细信息。 您还将知识库导出到 DQS 文件发布已更新前**供应商**知识库。  
  
1.  在主页面中的**DQS 客户端**，单击**右箭头**旁边**供应商**下**最近的知识库**单击**域管理**。  
  
2.  单击**联系人电子邮件**的域，然后切换到列表中**域值**右窗格中的选项卡。  
  
3.  单击**向下箭头**旁边**导入值**单击工具栏上的图标**导入项目值**。  
  
     ![导入项目值工具栏按钮](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "导入项目值工具栏按钮")  
  
4.  在中**导入项目值**对话框中，选择**Cleanse Supplier List**项目，然后单击**确定**。  
  
5.  注意，此时将导入所有电子邮件以及您在交互式清理过程中所做的两处更正内容。 滚动以查看这两处更正内容。  
  
    |ReplTest1|更正为|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  重复上述步骤导入项目值为**国家/地区**域，请注意，新条目添加用于更正**United State**到**美国**(与s)。  
  
    |ReplTest1|更正为|  
    |-----------|----------------|  
    |United State|United States|  
  
7.  若要查看旧域值，请清除**仅显示新**复选框。  
  
8.  重复上述步骤导入项目值为**Supplier Name**域。 默认情况下，在导入后，您将只看到新值。 若要查看所有值，请清除**仅显示新**复选框。 具有丰富**供应商**知识库的清理活动的学习的内容。 知识库越强，清理结果就越好。  
  
    > [!NOTE]  
    >  无法导入复合域的值。  
  
9. 单击**导出知识库**工具栏上的图标**导出知识库**。  
  
     ![导出知识库菜单](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "导出知识库菜单")  
  
10. 导航到 Tutorial 文件夹中，键入**Suppliers.dqs**有关**文件名**，然后单击**保存**。 您可以使用此 DQS 文件创建基于此文件的新知识库。  
  
11. 单击**确定**以关闭**导出知识库-Suppliers**消息框。  
  
12. 单击**完成**以完成活动。  
  
13. 单击“发布” 。  
  
14. 单击**确定**消息框上。  
  
## <a name="next-step"></a>下一步  
 [第 3 课：从供应商列表匹配数据以便删除重复项](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
