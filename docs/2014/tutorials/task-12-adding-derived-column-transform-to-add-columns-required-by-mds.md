---
title: 任务12：添加派生列转换以添加 MDS 所需的列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 18789f5bc1d97e1531588d50e2430829f95912b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65485243"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>任务 12：添加派生列转换以添加 MDS 所需的列
  在本任务中，您将向数据流添加派生列转换。 将两个派生列**ImportType**和**BatchTag**添加到传递给此转换的记录。 您应该在将数据上载到 MDS 中的临时表之前添加这些列。 这两列是 MDS 中的临时表所必需的列。 有关更多详细信息，请参阅[叶成员临时表](../master-data-services/leaf-member-staging-table-master-data-services.md)。  
  
1.  将从 " **SSIS 工具箱**" 中的 "**公共**" 部分拖放到 **"数据流" 选项卡**的**派生列转换**。  
  
2.  右键**单击 "数据流**" 选项卡中的 "**派生列**转换"，然后单击 "**重命名**"。 键入 "**添加 MDS 所需的列**"，然后按**enter**。  
  
3.  使用蓝色连接器连接**筛选器重复项**以**添加 MDS 所需的列**。 应会看到 "**输入输出选择**" 对话框。  
  
4.  在 "**输入输出选择**" 对话框中，选择 "**唯一记录**"，并单击 **"确定"**。  
  
     ![“选择输入输出”对话框](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "“选择输入输出”对话框")  
  
5.  单击菜单栏上的 " **SSIS** "，然后单击 "**变量**"。  
  
6.  在 "**变量**" 窗口中，单击工具栏上的 "**添加变量**" 按钮。  
  
     ![SSIS 变量窗口](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "SSIS 变量窗口")  
  
7.  键入**ImportType**作为**名称**，键入**2**作为**值**。 您将该值指定为 2，因为您想要向 MDS 中的实体添加新成员。 有关此参数的详细信息，请参阅[叶成员临时表](../master-data-services/leaf-member-staging-table-master-data-services.md)。  
  
8.  再次单击 "**添加变量**" 工具栏按钮。  
  
9. 键入 " **BatchTag** " 作为 "**名称**"，选择 "**字符串**" 作为 "**数据类型**"，并选择 " **EIMBatch** " 作为**值**。 **BatchTag**只是要提交到 MDS 的批处理的唯一名称。  
  
10. 在 "**数据流" 选项卡**中，双击 "**添加 MDS 所需的列**"。  
  
11. 在 "**派生列转换编辑器**" 对话框的**底部窗格的列表框**中，键入**ImportType**作为**派生列名称**。  
  
12. 展开左上方窗格中的 "**变量和参数**"，将**User：： ImportType**拖放到**Expression**列。  
  
     ![派生列转换编辑器](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "派生列转换编辑器")  
  
13. 在 "**派生列名称**" 的下一行中键入**BatchTag** 。  
  
14. 将**User：： BatchTag**从**Variables 和 Parameters**拖放到**Expression**列。  
  
15. 单击 **"确定"** 以关闭 "**派生列转换**" 对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 13：添加 OLE DB 目标以便将数据写入 MDS 临时表](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
