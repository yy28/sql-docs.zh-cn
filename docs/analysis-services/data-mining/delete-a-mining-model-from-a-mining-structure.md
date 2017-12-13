---
title: "从挖掘结构中删除挖掘模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], mining models
- deleting mining models
- removing mining models
- mining models [Analysis Services], deleting
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 470e1d74434261b08c47f93c060c4ac4da143cb2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>从挖掘结构中删除挖掘模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]你可以通过使用数据挖掘设计器中，通过使用删除挖掘模型[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，或通过使用 DMX 语句。  
  
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
  
-   [删除挖掘模型 (DMX)](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
