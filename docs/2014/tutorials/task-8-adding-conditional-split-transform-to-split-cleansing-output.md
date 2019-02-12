---
title: 任务 8:添加有条件拆分转换以拆分清理输出 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 401768ca9a811e9b9709127be391bb52de778b32
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024338"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>任务 8:添加有条件拆分转换以拆分清理输出
  在此转换中，您向数据流添加有条件拆分转换。 有条件拆分转换可以根据数据内容将行路由到不同的输出。 对于本教程中，你使用**记录状态**从 DQS 清理转换的输出列。 在本教程中，您将只向 MDS 服务器上载正确或已更正的记录。 因此，您可以检查**记录状态**是**更正**或**已更正**，和之前上载到 MDS 中合并的记录。  
  
1.  拖放**有条件拆分转换**从**常见**主题中**SSIS 工具箱**到**数据流**选项卡下**清理供应商数据**。  
  
2.  右键单击**有条件拆分**，然后单击**重命名**。 类型**选择正确和已更正的记录**然后按**ENTER**。  
  
3.  连接**清理供应商数据**并**选择正确和已更正的记录**使用蓝色连接器。  
  
     ![清理供应商数据-> 选择正确和已更正](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "清理供应商数据-> 选择正确和已更正")  
  
4.  双击**选择正确和已更正的记录**中**数据流**选项卡。  
  
5.  更改**默认输出名称**到屏幕底部**更正**。  
  
6.  展开**列**中**左上方的窗格**。  
  
     ![有条件拆分转换编辑器](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "有条件拆分转换编辑器")  
  
7.  拖放**记录状态**到**条件**列。  
  
8.  类型 **= ="已更正"** 旁边 **[记录状态]** 有关**条件**列。  
  
9. 单击**案例 1**中**输出名称列**，并将名称更改为**已更正**。  
  
10. 单击**确定**以关闭**有条件拆分转换编辑器**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 9:添加 Union All 转换以合并正确和已更正的记录](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
