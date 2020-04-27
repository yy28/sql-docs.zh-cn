---
title: 任务9：添加 Union All 转换以合并正确和已更正的记录 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489657"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>任务 9：添加 Union All 转换以合并正确和已更正的记录
  在本任务中，您将向数据流添加 Union All 转换。 Union All 转换将多个输入组合到一个输出中。 在您的方案中，它将正确记录和已更正的记录合并到一个流中。  
  
1.  将 " **SSIS 工具箱**" 的 "**通用**" 部分中的 "**合并所有**转换" 拖放到 "**数据流" 选项**卡，然后在 "**选择正确和已更正的记录**" 下放置。  
  
2.  右键**单击 "数据流**" 选项卡中的 " **Union All**转换"，然后单击 "**重命名**"。 键入 "**合并正确和已更正的记录**"，然后按**enter**。  
  
     ![合并正确和已更正的记录](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "合并正确和已更正的记录")  
  
3.  "连接"**选择正确和已更正的记录**，以便在 "**数据流" 选项卡**中使用蓝色连接器**合并正确和更正的记录**。 应会看到 "**输入输出选择**" 对话框。  
  
4.  在 "**输入输出**" 对话框中，为 "**输出**" 选择 "**正确**"，然后单击 **"确定"**。  
  
     ![“选择输入输出”对话框](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "“选择输入输出”对话框")  
  
5.  将标题为 "**正确**" 的连接线拖放到左侧的连接符末尾处。  
  
     ![连接正确的以合并正确和已更正的记录](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "连接正确的以合并正确和已更正的记录")  
  
6.  如果选择 "选择**正确和已更正的记录**" 转换，应会看到另一个蓝色连接器。 拖动该蓝色连接器以**合并正确和已更正的记录**。  
  
     ![连接已更正的以合并正确和已更正的记录](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "连接已更正的以合并正确和已更正的记录")  
  
7.  应**更正**此**连接器**的标题。 由于只有两个条件是**正确**的并且已**更正**，并且已经使用了一个条件，此时不会显示 "**输入输出选择**" 对话框。 如果连接器重叠，则通过将连接器向左或向右拖将一个连接器向左移，将另一个连接器向右移。  
  
## <a name="next-step"></a>下一步  
 [任务 10：添加模糊分组转换以确定重复项](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
