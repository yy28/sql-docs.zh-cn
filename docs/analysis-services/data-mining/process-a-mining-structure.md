---
title: "处理挖掘结构 | Microsoft Docs"
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
  - "挖掘结构 [Analysis Services], 处理"
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 31
---
# 处理挖掘结构
  必须先部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目并处理挖掘结构和挖掘模型，然后才能浏览或使用与挖掘结构关联的挖掘模型。 此外，如果更改了挖掘结构或挖掘模型，则系统会提示您重新对其进行部署和处理。 处理 **中数据挖掘设计器的** “挖掘结构” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 选项卡中的结构时，也会处理所有关联的模型。  
  
 可以使用这些工具处理挖掘结构：  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA：“处理”命令  
  
 有关如何处理单个模型的信息，请参阅[处理挖掘模型](../../analysis-services/data-mining/process-a-mining-model.md)。  
  
### 使用 SQL Server Data Tools 处理挖掘结构和所有关联的挖掘模型  
  
1.  从 **中的** “挖掘模型” **菜单项中，选择** “处理挖掘结构和所有模型” [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。  
  
     如果更改了结构，则在处理模型之前，系统会提示您重新部署该结构。 单击 **“是”**。  
  
2.  在“处理挖掘结构 - \<结构>”对话框中，单击“运行”。  
  
     **“处理进度”** 对话框将打开以显示有关模型处理的详细信息。  
  
3.  模型处理完成后，在 **“处理进度”** 对话框中单击 **“关闭”** 。  
  
4.  在“处理挖掘结构 - \<结构>”对话框中，单击“关闭”。  
  
## 另请参阅  
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  