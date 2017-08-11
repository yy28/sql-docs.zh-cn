---
title: "第 7 课： 在父报表上添加钻取操作 |Microsoft 文档"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: aad2da1a-d7b1-4afa-a66a-1ff102e8306f
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9a9790c4afc44e66c521005a3556f8082527d260
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-7-add-drillthrough-action-on-parent-report"></a>第 7 课：在父报表上添加钻取操作
向网站应用程序添加 ReportViewer 控件后，接下来要在父报表上添加钻取操作。  
  
### <a name="to-add-drillthrough-action-on-the-parent-report"></a>在父报表上添加钻取操作  
  
1.  转到父报表。  
  
2.  选择包含的值文本框中**名称**。  
  
3.  文本框中，右键单击，然后选择**文本框属性**。  
  
4.  转到**操作**选项卡上，然后选择**转到报表**选项。  
  
5.  输入中的子报表的名称**指定报表**部分。  
  
    > [!NOTE]
    > 请勿包括报表名称的文件扩展名。  
  
6.  选择**添加**下**使用这些参数运行报表**部分。  
  
7.  类型**productid**中**名称**框中，，然后选择**ProductID**中**值**下拉列表。  
  
8.  选择**确定**完成。  
  
## <a name="next-task"></a>下一个任务  
您已成功地在父报表上添加了钻取操作。 接下来，将创建一个数据筛选器，用于为子报表定义的数据表。 请参阅 [第 8 课：创建数据筛选器](../reporting-services/lesson-8-create-a-data-filter.md)。  
  
  
  


