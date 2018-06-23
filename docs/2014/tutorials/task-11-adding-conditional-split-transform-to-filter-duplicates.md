---
title: 任务 11： 添加条件拆分转换筛选重复项 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7f61fa706659a6f71b2c69f18bcf7b694993ed00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028473"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>任务 11：添加有条件拆分转换以筛选重复项
  在本任务中，您将向数据流添加有条件拆分转换。 此转换帮助您从传入的记录集筛选重复项。 模糊分组转换将它找到的记录分组为匹配项并选择其中一个记录作为透视记录。 组中的所有记录都具有相同的 _key_out 值。 组中的透视记录具有与 _key_out 值相同的 _key_in。 组中的其他记录的 _key_in 和 _key_out 值不同。 因此，当使用条件 _key_in==_key_out 筛选时，只能得到组中的透视行。  
  
1.  拖放**有条件拆分**转换从**常见**主题中**SSIS 工具箱**到**数据流**选项卡。  
  
2.  右键单击**条件拆分转换**中**数据流**卡，然后单击**重命名**。 类型**筛选器重复**按**ENTER**。  
  
3.  连接**组具有匹配 Id 的供应商**到**筛选重复项**。  
  
4.  双击**筛选器重复**以启动**条件拆分转换编辑器**对话框。  
  
5.  展开**列**在左上方窗格中。  
  
6.  拖放 **_key_in**到**条件**列。  
  
7.  类型 = = （等于） 旁边 **_key_in**和拖放 **_key_out**。  
  
8.  单击**情况 1**中**输出名称**列中，键入**唯一记录**，按**ENTER**。  
  
     ![有条件拆分转换编辑器](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "有条件拆分转换编辑器")  
  
9. 单击**确定**关闭**有条件拆分转换编辑器**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 12：添加派生列转换以添加 MDS 所需的列](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  