---
title: 任务 9：添加 Union All 转换以合并正确和已更正的记录 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b160b6e513ad866126df8b401b82ee1270be84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489657"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>任务 9：添加 Union All 转换以合并正确和已更正的记录
  在本任务中，您将向数据流添加 Union All 转换。 Union All 转换将多个输入组合到一个输出中。 在您的方案中，它将正确记录和已更正的记录合并到一个流中。  
  
1.  拖放**Union All**从转换**常见**一部分**SSIS 工具箱**到**数据流**选项卡上，并将其放在**选择正确和已更正的记录**。  
  
2.  右键单击**Union All**转换中**数据流**选项卡，然后单击**重命名**。 类型**合并正确和已更正的记录**，然后按**ENTER**。  
  
     ![合并正确和已更正的记录](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "合并正确和已更正的记录")  
  
3.  连接**选择正确和已更正的记录**到**合并正确和已更正的记录**中**数据流**选项卡上使用蓝色连接器。 应会看到**选择输入输出**对话框。  
  
4.  在**输入输出**对话框中，选择**更正**有关**输出**然后单击**确定**。  
  
     ![输入输出选择对话框](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "输入输出选择对话框")  
  
5.  将标题为该连接器移**更正**通过拖放到左的连接器的末尾处的点左侧。  
  
     ![连接正确的以合并正确和已更正](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "连接正确的以合并正确和已更正")  
  
6.  如果选择**选择正确和已更正的记录**转换，应会看到另一个蓝色连接器。 将为该蓝色连接器拖**合并正确和已更正的记录**。  
  
     ![连接已更正的以合并正确和已更正](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "连接已更正的以合并正确和已更正")  
  
7.  这**连接器**应名为**已更正**。 由于有只有两个条件**更正**并**已更正**，并已使用一个条件，则**选择输入输出**对话框不显示这一次。 如果连接器重叠，则通过将连接器向左或向右拖将一个连接器向左移，将另一个连接器向右移。  
  
## <a name="next-step"></a>下一步  
 [任务 10:添加模糊分组转换以确定重复项](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
