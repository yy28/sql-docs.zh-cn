---
title: 第 4 课： 标记为日期表 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a2a6ce44a66fbb1e9045116580acc726f648df9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265743"
---
# <a name="lesson-4-mark-as-date-table"></a>第 4 课：标记为日期表
  在“第 2 课：添加数据”中，您导入了名为 DimDate 的维度表。 然后您在“第 3 课：重命名列”中将 DimDate 表重命名为简单的 Date。 虽然在模型中该表已命名为 Date，它也可以称为“日期表”，该表中包含日期和时间数据。  
  
 每当在计算中使用时间智能函数（和稍后创建度量值时所要做的一样），必须指定日期表属性，其中包括“日期表”和该表中的唯一标识符“日期列”。 您然后可以创建其他表和日期表之间的有效关系，这对于使用 DAX 时间智能函数的计算是必需的。  
  
 在本课中，将导入和重命名的 Date 表标记为“日期表”，将 Date 列（Date 表中）标记为“日期列”（唯一标识符）。 全部使用名称 Date 可能导致一些混淆，但是您很快就会理解。  
  
 学完本课的估计时间： **3 分钟**  
  
## <a name="prerequisites"></a>必要條件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 执行本课中的任务之前，应已完成上一课： [第 3 课：重命名列](rename-columns.md)。  
  
### <a name="to-set-mark-as-date-table"></a>标记为日期表  
  
1.  在模型设计器中，单击“Date”表（选项卡）。  
  
2.  单击“表”菜单，然后依次单击“日期”和“标记为日期表”。  
  
3.  在“标记为日期表”对话框的“日期”列表框中，选择“日期”列作为唯一标识符。  
  
## <a name="next-steps"></a>后续步骤  
 若要继续学习本教程，请转到下一课： [第 5 课：创建关系](lesson-4-create-relationships.md)。  
  
  
