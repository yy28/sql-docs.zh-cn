---
title: 任务 12： 添加派生列转换添加列所需的 MDS |Microsoft 文档
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
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b81dd18f0ba79167a66b5cdd09c2059fcd0e0a96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128438"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>任务 12：添加派生列转换以添加 MDS 所需的列
  在本任务中，您将向数据流添加派生列转换。 添加两个派生的列， **ImportType**和**BatchTag**到记录传递给此转换。 您应该在将数据上载到 MDS 中的临时表之前添加这些列。 这两列是 MDS 中的临时表所必需的列。 请参阅[叶成员临时表](http://msdn.microsoft.com/library/ee633854.aspx)有关详细信息。  
  
1.  拖放**派生列转换**从**常见**主题中**SSIS 工具箱**到**数据流**选项卡。  
  
2.  右键单击**派生列**在中转换**数据流**卡，然后单击**重命名**。 类型**添加列所需的 MDS**按**ENTER**。  
  
3.  连接**筛选器重复**到**添加列所需的 MDS**使用蓝色的连接器。 你应该会看到**输入输出选择**对话框。  
  
4.  在**输入输出选择**对话框中，选择**唯一记录**，然后单击**确定**。  
  
     ![输入输出选择对话框](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "输入输出选择对话框中")  
  
5.  单击**SSIS**单击菜单栏上**变量**。  
  
6.  在**变量**窗口中，单击**添加变量**工具栏上的按钮。  
  
     ![SSIS 变量窗口](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "SSIS 变量窗口")  
  
7.  类型**ImportType**为**名称**和**2**为**值**。 您将该值指定为 2，因为您想要向 MDS 中的实体添加新成员。 有关此参数的详细信息，请参阅[叶成员临时表](http://msdn.microsoft.com/library/ee633854.aspx)。  
  
8.  单击**添加变量**再次工具栏按钮。  
  
9. 类型**BatchTag**为**名称**，选择**字符串**为**数据类型**，和**EIMBatch**为**值**。 **BatchTag**是只需为你将提交到 MDS 批的唯一名称。  
  
10. 在**数据流**选项卡上，双击**添加列所需的 MDS**。  
  
11. 在**派生列转换编辑器**对话框中，在**底部窗格中的列表框**，类型**ImportType**为**派生列名称**.  
  
12. 展开**变量和参数**在左上方窗格中，拖放**User::ImportType**到**表达式**列。  
  
     ![派生列转换编辑器](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "派生列转换编辑器")  
  
13. 类型**BatchTag**中的下一行**派生列名称**。  
  
14. 拖放**User::BatchTag**从**变量和参数**到**表达式**列。  
  
15. 单击**确定**关闭**Derived Column Transformation**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 13：添加 OLE DB 目标以便将数据写入 MDS 临时表](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  