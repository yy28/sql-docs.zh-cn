---
title: "更改数据挖掘查询的超时值 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
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
helpviewer_keywords: time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0d04cbc253fea4d12c142c4f755ffef2653fcd0b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>更改数据挖掘查询的超时值
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在生成提升图或执行预测查询时，有时它可能需要很长时间才能生成预测所需的所有数据。 为防止查询超时，您可以更改控制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器要等待完成查询的时间值。  
  
 默认值为 15；不过，如果您的模型比较复杂或者数据源较大，此值可能不够。 如果必要，可以大幅增大该值，以便有足够的时间进行处理。 例如，如果将 **“查询超时值”** 设置为 600，则查询可以持续运行 10 分钟之久。  
  
 有关预测查询的详细信息，请参阅 [数据挖掘查询任务和操作指南](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)。  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>配置数据挖掘查询的超时值  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，从 **“工具”** 菜单中选择 **“选项”**。  
  
2.  在 **“选项”** 窗格中，展开 **“商业智能设计器”**。  
  
3.  单击 **“查询超时值”** 文本框，然后键入一个秒数值。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘查询任务和操作指南](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
