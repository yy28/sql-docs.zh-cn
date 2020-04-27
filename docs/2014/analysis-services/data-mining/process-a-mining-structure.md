---
title: 处理挖掘结构 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], processing
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92793adcf2fd04b1dac0c26933c1d5969a31f1a5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083112"
---
# <a name="process-a-mining-structure"></a>处理挖掘结构
  必须先部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目并处理挖掘结构和挖掘模型，然后才能浏览或使用与挖掘结构关联的挖掘模型。 此外，如果更改了挖掘结构或挖掘模型，则系统会提示您重新对其进行部署和处理。 处理 **中数据挖掘设计器的** “挖掘结构” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 选项卡中的结构时，也会处理所有关联的模型。  
  
 可以使用这些工具处理挖掘结构：  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA：“处理”命令  
  
 有关如何处理单个模型的信息，请参阅 [处理挖掘模型](process-a-mining-model.md)。  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>使用 SQL Server Data Tools 处理挖掘结构和所有关联的挖掘模型  
  
1.  从 **中的** “挖掘模型” **菜单项中，选择** “处理挖掘结构和所有模型” [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。  
  
     如果更改了结构，则在处理模型之前，系统会提示您重新部署该结构。 单击 **“是”** 。  
  
2.  在 "**处理挖掘结构- \<结构>** " 对话框中，单击 "**运行**"。  
  
     **“处理进度”** 对话框将打开以显示有关模型处理的详细信息。  
  
3.  模型处理完成后，在 **“处理进度”** 对话框中单击 **“关闭”** 。  
  
4.  在 "**处理挖掘结构- \<结构>** " 对话框中单击 "**关闭**"。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘结构任务和操作指南](mining-structure-tasks-and-how-tos.md)  
  
  
