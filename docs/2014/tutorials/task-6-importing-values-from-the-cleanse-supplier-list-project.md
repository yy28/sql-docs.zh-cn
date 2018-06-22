---
title: 任务 6： 导入从值清理供应商列表项目 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7a915013d779392d585bd5609384fab7bffd2800
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017446"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>任务 6：从 Cleanse Supplier List 项目导入值
  在该任务中，您将导入在清理过程中收集的数据质量知识。 请参阅[清理项目值导入到域中](http://msdn.microsoft.com/library/hh479581.aspx)更多详细信息的主题。 你还将知识库导出到 DQS 文件在发布更新之前**供应商**知识库。  
  
1.  在主页面中的**DQS 客户端**，单击**右箭头**旁边**供应商**下**最近的知识库**单击**域管理**。  
  
2.  单击**联系人电子邮件**的域，再切换到列表中**域值**右窗格中的选项卡。  
  
3.  单击**向下箭头**旁边**导入值**在工具栏上单击图标**导入项目值**。  
  
     ![导入项目值工具栏按钮](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "导入项目值工具栏按钮")  
  
4.  在**导入项目值**对话框中，选择**清理供应商列表**项目，然后单击**确定**。  
  
5.  注意，此时将导入所有电子邮件以及您在交互式清理过程中所做的两处更正内容。 滚动以查看这两处更正内容。  
  
    |ReplTest1|更正为|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  重复上一步的导入项目值**国家/地区**域，请注意，新条目添加用于更正**美国状态**到**美国**(与s)。  
  
    |ReplTest1|更正为|  
    |-----------|----------------|  
    |United State|United States|  
  
7.  若要查看的旧的域值，请清除**仅显示新**复选框。  
  
8.  重复上一步的导入项目值**供应商名称**域。 默认情况下，在导入后，您将只看到新值。 若要查看所有值，请清除**仅显示新**复选框。 在更新**供应商**与你所了解的从清理活动的知识库。 知识库越强，清理结果就越好。  
  
    > [!NOTE]  
    >  无法导入复合域的值。  
  
9. 单击**导出知识库**工具栏上的图标**导出知识库**。  
  
     ![导出知识库菜单](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "导出知识库菜单")  
  
10. 导航到教程的文件夹中，类型**Suppliers.dqs**为**文件名**，然后单击**保存**。 您可以使用此 DQS 文件创建基于此文件的新知识库。  
  
11. 单击**确定**关闭**导出知识库 – 供应商**消息框。  
  
12. 单击**完成**完成活动。  
  
13. 单击“发布” 。  
  
14. 单击**确定**消息框上。  
  
## <a name="next-step"></a>下一步  
 [第 3 课：匹配数据以便从供应商列表中删除重复项](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  