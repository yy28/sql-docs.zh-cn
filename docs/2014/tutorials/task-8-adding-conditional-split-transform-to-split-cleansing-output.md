---
title: 任务 8： 添加条件拆分转换拆分清理输出 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6dc3b98e03a7940841bc97012c1a4e4220bb970d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124024"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>任务 8：添加有条件拆分转换以拆分清理输出
  在此转换中，您向数据流添加有条件拆分转换。 有条件拆分转换可以根据数据内容将行路由到不同的输出。 对于本教程中，你使用**记录状态**从 DQS 清理转换的输出列。 在本教程中，您将只向 MDS 服务器上载正确或已更正的记录。 因此如果您检查**记录状态**是**更正**或**已更正**，并将记录合并到 MDS 上载记录之前。  
  
1.  拖放**条件拆分转换**从**常见**主题中**SSIS 工具箱**到**数据流**选项卡下**清理供应商数据**。  
  
2.  右键单击**有条件拆分**，然后单击**重命名**。 类型**选取正确和更正的记录**按**ENTER**。  
  
3.  连接**清理供应商数据**和**选取正确和更正的记录**使用蓝色的连接器。  
  
     ![清理供应商数据-> 选取正确的和已更正](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "清理供应商数据-> 选取正确的和已更正")  
  
4.  双击**选取正确和更正的记录**中**数据流**选项卡。  
  
5.  更改**默认输出名称**到屏幕底部**更正**。  
  
6.  展开**列**中**左上窗格**。  
  
     ![有条件拆分转换编辑器](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "有条件拆分转换编辑器")  
  
7.  拖放**记录状态**到**条件**列。  
  
8.  类型 **= ="已更正"** 旁边 **[记录状态]** 为**条件**列。  
  
9. 单击**情况 1**中**输出名称列**，和名称更改为**已更正**。  
  
10. 单击**确定**关闭**有条件拆分转换编辑器**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 9：添加 Union All 转换以合并正确和已更正的记录](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  