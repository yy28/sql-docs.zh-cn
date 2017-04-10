---
title: "从挖掘结构中删除挖掘模型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "挖掘结构 [Analysis Services], 挖掘模型"
  - "删除挖掘模型"
  - "删除挖掘模型"
  - "挖掘模型 [Analysis Services], 删除"
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 29
---
# 从挖掘结构中删除挖掘模型
  您可以使用数据挖掘设计器、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 DMX 语句删除挖掘模型。  
  
### 使用 SQL Server Data Tools 删除挖掘模型  
  
1.  在 **中，选择** “挖掘模型” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡。  
  
2.  右键单击要删除的模型，然后选择“删除”。  
  
     将打开 **“删除对象”** 对话框。  
  
3.  单击 **“确定”**。  
  
### 使用 SQL Server Management Studio 删除挖掘模型  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开包含模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
2.  展开 **“挖掘结构”**，然后展开 **“挖掘模型”**。  
  
3.  右键单击要删除的模型，然后选择“删除”。  
  
     删除模型并不删除定型数据，只删除定型时创建的元数据和所有模式。  
  
### 使用 DMX 删除挖掘模型  
  
-   [删除挖掘模型 (DMX)](../../dmx/drop-mining-model-dmx.md)  
  
## 另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  