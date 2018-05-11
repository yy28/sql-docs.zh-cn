---
title: 从挖掘结构中删除挖掘模型 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e67e78ff0f3faf2d8a9b468dd2ecc76506c0e80
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>从挖掘结构中删除挖掘模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以使用数据挖掘设计器、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 DMX 语句删除挖掘模型。  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>使用 SQL Server Data Tools 删除挖掘模型  
  
1.  在 **中，选择** “挖掘模型” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡。  
  
2.  右键单击要删除的模型，然后选择“删除”。  
  
     将打开 **“删除对象”** 对话框。  
  
3.  单击 **“确定”**。  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 删除挖掘模型  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开包含模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
2.  展开 **“挖掘结构”**，然后展开 **“挖掘模型”**。  
  
3.  右键单击要删除的模型，然后选择“删除”。  
  
     删除模型并不删除定型数据，只删除定型时创建的元数据和所有模式。  
  
### <a name="delete-a-mining-model-using-dmx"></a>使用 DMX 删除挖掘模型  
  
-   [删除挖掘模型 & #40; DMX & #41;](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
