---
title: "创建数据挖掘维度 | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "挖掘结构 [Analysis Services], 维度"
ms.assetid: 9f0c39e5-3516-43ab-b203-f3f6dbcff89a
caps.latest.revision: 12
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 12
---
# 创建数据挖掘维度
  如果挖掘结构基于 OLAP 多维数据集，则可以创建包含挖掘模型内容的维度。 然后可以将维度合并回源多维数据集。  
  
 还可以浏览维度、使用维度浏览模型结果或使用 MDX 查询维度。  
  
### 创建数据挖掘维度  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的数据挖掘设计器中，选择 **“挖掘结构”** 选项卡或 **“挖掘模型”** 选项卡。  
  
2.  从 **“挖掘模型”** 菜单中，选择 **“创建数据挖掘维度”**。  
  
     将打开 **“创建数据挖掘维度”** 对话框。  
  
3.  在 **“创建数据挖掘维度”** 对话框的 **“模型名称”** 列表中，选择 OLAP 挖掘模型。  
  
4.  在 **“维度名称”** 框中，输入新的数据挖掘维度的名称。  
  
5.  如果要创建包含新的数据挖掘维度的多维数据集，则选择 **“创建多维数据集”**。 选择 **“创建多维数据集”**之后，可以输入多维数据集的新名称。  
  
6.  单击 **“确定”**。  
  
     这样便可创建数据挖掘维度并将其添加到解决方案资源管理器中的 **“维度”** 文件夹。 如果选择了 **“创建多维数据集”**，则也可创建新的多维数据集并将其添加到 **“多维数据集”** 文件夹。  
  
## 另请参阅  
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  