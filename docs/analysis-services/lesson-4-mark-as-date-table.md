---
title: "第 4 课：标记为日期表 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 4 课：标记为日期表
在“第 2 课：添加数据”中，导入了名为 DimDate 的维度表，并将其重命名为 Date。 虽然在模型中该表已命名为 Date，它也可以称为“日期表”，该表中包含日期和时间数据。  
  
每当在计算中使用时间智能函数（和稍后创建度量值时所要做的一样），必须指定日期表属性，其中包括“日期表”和该表中的唯一标识符“日期列”。 您然后可以创建其他表和日期表之间的有效关系，这对于使用 DAX 时间智能函数的计算是必需的。  
  
在本课中，将导入和重命名的 Date 表标记为“日期表”，将 Date 列（Date 表中）标记为“日期列”（唯一标识符）。 全部使用名称 Date 可能导致一些混淆，但是您很快就会理解。  
  
学完本课的估计时间：**3 分钟**  
  
## 先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 执行本课中的任务之前，应已完成上一课：[第 3 课：重命名列](../analysis-services/lesson-3-rename-columns.md)。  
  
### 标记为日期表  
  
1.  在模型设计器中，单击“Date”表（选项卡）。  
  
2.  选择“日期”列，然后在“属性”窗口的“数据类型”下面确保已选中“日期”。  
  
3.  单击“表”菜单，然后依次单击“日期”和“标记为日期表”。  
  
4.  在“标记为日期表”对话框的“日期”列表框中，选择“日期”列作为唯一标识符。  
  
## 后续步骤  
若要继续学习本教程，请转到下一课：[第 5 课：创建关系](../analysis-services/lesson-5-create-relationships.md)。  
  
  
  
