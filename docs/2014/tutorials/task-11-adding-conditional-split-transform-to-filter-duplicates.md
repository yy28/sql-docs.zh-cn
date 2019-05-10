---
title: 任务 11：添加有条件拆分转换以筛选重复项 |Microsoft Docs
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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476754"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>任务 11：添加有条件拆分转换以筛选重复项
  在本任务中，您将向数据流添加有条件拆分转换。 此转换帮助您从传入的记录集筛选重复项。 模糊分组转换将它找到的记录分组为匹配项并选择其中一个记录作为透视记录。 组中的所有记录都具有相同的 _key_out 值。 组中的透视记录具有与 _key_out 值相同的 _key_in。 组中的其他记录的 _key_in 和 _key_out 值不同。 因此，当使用条件 _key_in==_key_out 筛选时，只能得到组中的透视行。  
  
1.  拖放**有条件拆分**从转换**常见**主题中**SSIS 工具箱**到**数据流**选项卡。  
  
2.  右键单击**有条件拆分转换**中**数据流**选项卡，然后单击**重命名**。 类型**筛选重复项**然后按**ENTER**。  
  
3.  连接**分组具有匹配 Id 的供应商**到**筛选重复项**。  
  
4.  双击**筛选重复项**以启动**条件拆分转换编辑器**对话框。  
  
5.  展开**列**左上方窗格中。  
  
6.  拖放 **_key_in**到**条件**列。  
  
7.  类型 = = （等于） 旁边 **_key_in**拖放 **_key_out**。  
  
8.  单击**案例 1**中**输出的名称**列中，键入**唯一记录**，然后按**ENTER**。  
  
     ![有条件拆分转换编辑器](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "有条件拆分转换编辑器")  
  
9. 单击**确定**以关闭**有条件拆分转换编辑器**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 12:添加派生列转换以添加 MDS 所需的列](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
