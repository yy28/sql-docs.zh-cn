---
title: 任务8：添加有条件拆分转换以拆分清理输出 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d5a55f0694094e6fe88a42946bcff34f420210f4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489674"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>任务 8：添加有条件拆分转换以拆分清理输出
  在此转换中，您向数据流添加有条件拆分转换。 有条件拆分转换可以根据数据内容将行路由到不同的输出。 对于本教程，请使用 DQS 清理转换中的 "**记录状态**" 输出列。 在本教程中，您将只向 MDS 服务器上载正确或已更正的记录。 因此，您需要检查**记录状态**是否**正确**，**并**在将记录上载到 MDS 之前合并记录。  
  
1.  从 " **SSIS 工具箱**" 中的 "**公共**" 部分拖放到 "**清理供应商数据**" 下**的 "数据流**" 选项**卡中。**  
  
2.  右键单击 "**条件拆分**"，然后单击 "**重命名**"。 键入 "**选择正确和已更正的记录**"，然后按**enter**。  
  
3.  连接**清理供应商数据**，并使用蓝色连接器**选择正确和更正的记录**。  
  
     ![清理供应商数据-> 选取正确的 & 更正](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "清理供应商数据 -> 选择正确和已更正的记录")  
  
4.  双击 **"数据流" 选项**卡中的 "**选择正确和已更正的记录**"。  
  
5.  更改屏幕底部的**默认输出名称**以**更正**。  
  
6.  在**左上方窗格**中展开 "**列**"。  
  
     ![有条件拆分转换编辑器](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "有条件拆分转换编辑器")  
  
7.  将**记录状态**拖放到 "**条件**" 列。  
  
8.  对于 "**条件**"**列，Type** **= = "更正"** 。  
  
9. 单击 "**输出名称" 列**中的 "**事例 1** "，然后将名称更改为 "已**更正**"。  
  
10. 单击 **"确定"** 以关闭 "有**条件拆分转换编辑器**" 对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 9：添加 Union All 转换以合并正确和已更正的记录](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
