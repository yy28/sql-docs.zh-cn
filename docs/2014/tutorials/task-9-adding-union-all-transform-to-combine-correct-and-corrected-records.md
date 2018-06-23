---
title: 任务 9： 添加 Union All 转换要合并的正确和更正记录 |Microsoft 文档
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
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: df61e9219c179ab934a33a78f13499351047bf4b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129999"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>任务 9：添加 Union All 转换以合并正确和已更正的记录
  在本任务中，您将向数据流添加 Union All 转换。 Union All 转换将多个输入组合到一个输出中。 在您的方案中，它将正确记录和已更正的记录合并到一个流中。  
  
1.  拖放**Union All**转换从**常见**部分**SSIS 工具箱**到**数据流**选项卡上，并将其放在**选取正确和更正记录**。  
  
2.  右键单击**Union All**在中转换**数据流**卡，然后单击**重命名**。 类型**正确合并和更正的记录**，按**ENTER**。  
  
     ![合并正确和更正 Reocrds](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "组合正确和更正 Reocrds")  
  
3.  连接**选取正确和更正的记录**到**正确合并和更正的记录**中**数据流**选项卡上使用蓝色的连接器。 你应该会看到**输入输出选择**对话框。  
  
4.  在**输入输出**对话框中，选择**更正**为**输出**单击**确定**。  
  
     ![输入输出选择对话框](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "输入输出选择对话框中")  
  
5.  移动标题为连接器**更正**通过拖放到左连接器末尾的点的左侧。  
  
     ![连接到合并正确和更正正确](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "连接正确的组合正确和更正")  
  
6.  如果你选择**选取正确和更正的记录**转换，你应看到另一个蓝色连接器。 拖动到该蓝色连接器**正确合并和更正的记录**。  
  
     ![连接到合并正确和更正已更正](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "连接到合并正确和更正已更正")  
  
7.  这**连接器**应标题为**已更正**。 由于只有两个条件**更正**和**已更正**，并且已使用一个条件，则**输入输出选择**对话框中未显示这一次。 如果连接器重叠，则通过将连接器向左或向右拖将一个连接器向左移，将另一个连接器向右移。  
  
## <a name="next-step"></a>下一步  
 [任务 10：添加模糊分组转换以确定重复项](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  