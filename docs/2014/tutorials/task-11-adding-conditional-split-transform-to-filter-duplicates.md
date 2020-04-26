---
title: 任务11：添加有条件拆分转换以筛选重复项 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 71b050e49440764d355d4658607600c135741f50
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65476754"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>任务 11：添加有条件拆分转换以筛选重复项
  在本任务中，您将向数据流添加有条件拆分转换。 此转换帮助您从传入的记录集筛选重复项。 模糊分组转换将它找到的记录分组为匹配项并选择其中一个记录作为透视记录。 组中的所有记录都具有相同的 _key_out 值。 组中的透视记录具有与 _key_out 值相同的 _key_in。 组中的其他记录的 _key_in 和 _key_out 值不同。 因此，当使用条件 _key_in==_key_out 筛选时，只能得到组中的透视行。  
  
1.  从 " **SSIS 工具箱**" 中的 "**公共**" 部分**拖放到**"**数据流" 选项卡**上。  
  
2.  右键单击 "数据流 **" 选项卡**中的 "有**条件拆分转换**"，然后单击 "**重命名**"。 键入**筛选器重复项**，然后按**enter**。  
  
3.  连接**组具有匹配 id 的供应商**以**筛选重复项**。  
  
4.  双击 "**筛选重复项**" 以启动 "有**条件拆分转换编辑器**" 对话框。  
  
5.  在左上方窗格中展开 "**列**"。  
  
6.  将 **_key_in**拖放到 "**条件**" 列。  
  
7.  键入 = = （等于），然后 **_key_in**并拖放 **_key_out**。  
  
8.  单击 "**输出名称**" 列中的 "**事例 1** "，键入 "**唯一记录**"，然后按**enter**。  
  
     ![有条件拆分转换编辑器](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "有条件拆分转换编辑器")  
  
9. 单击 **"确定"** 以关闭 "有**条件拆分转换编辑器**" 对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 12：添加派生列转换以添加 MDS 所需的列](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
