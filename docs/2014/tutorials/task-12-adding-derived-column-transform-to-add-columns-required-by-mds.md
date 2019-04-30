---
title: 任务 12：添加派生列转换以添加 MDS 所需的列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c80f719bd756a0ad241ef270507e638b08c2081
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222618"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>任务 12：添加派生列转换以添加 MDS 所需的列
  在本任务中，您将向数据流添加派生列转换。 添加两个派生的列**ImportType**并**BatchTag**到记录传递给此转换。 您应该在将数据上载到 MDS 中的临时表之前添加这些列。 这两列是 MDS 中的临时表所必需的列。 请参阅[叶成员临时表](../master-data-services/leaf-member-staging-table-master-data-services.md)的更多详细信息。  
  
1.  拖放**派生列转换**从**常见**主题中**SSIS 工具箱**到**数据流**选项卡。  
  
2.  右键单击**派生列**转换中**数据流**选项卡，然后单击**重命名**。 类型**添加列所需的 MDS**然后按**ENTER**。  
  
3.  连接**筛选重复项**到**添加列所需的 MDS**使用蓝色连接器。 应会看到**选择输入输出**对话框。  
  
4.  在中**选择输入输出**对话框中，选择**唯一记录**，然后单击**确定**。  
  
     ![输入输出选择对话框](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "输入输出选择对话框")  
  
5.  单击**SSIS**在菜单栏上单击**变量**。  
  
6.  在中**变量**窗口中，单击**添加变量**工具栏上的按钮。  
  
     ![SSIS 变量窗口](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "SSIS 变量窗口")  
  
7.  类型**ImportType**有关**名称**并**2**有关**值**。 您将该值指定为 2，因为您想要向 MDS 中的实体添加新成员。 有关此参数的详细信息，请参阅[叶成员临时表](../master-data-services/leaf-member-staging-table-master-data-services.md)。  
  
8.  单击**添加变量**再次工具栏按钮。  
  
9. 类型**BatchTag**有关**名称**，选择**字符串**有关**数据类型**，并**EIMBatch**为**值**。 **BatchTag**是只需将提交到 MDS 的批处理的唯一名称。  
  
10. 在中**Data Flow**选项卡上，双击**添加列所需的 MDS**。  
  
11. 在中**派生列转换编辑器**对话框中**底部窗格中的列表框**，类型**ImportType**为**派生列名称**.  
  
12. 展开**变量和参数**左上方窗格中拖放**user:: importtype**到**表达式**列。  
  
     ![派生列转换编辑器](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "派生列转换编辑器")  
  
13. 类型**BatchTag**中的下一步行**派生列名称**。  
  
14. 拖放**user:: batchtag**从**变量和参数**到**表达式**列。  
  
15. 单击**确定**以关闭**派生列转换**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 13:添加 OLE DB 目标将数据写入 MDS 临时表](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
