---
title: 更改数据挖掘查询的超时值 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e6286a931c0e1ad27a99462853c3b8dfe6de36bc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>更改数据挖掘查询的超时值
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在生成提升图或执行预测查询时，生成预测所需的所有数据有时可能需要很长时间。 为防止查询超时，您可以更改控制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器要等待完成查询的时间值。  
  
 默认值为 15；不过，如果您的模型比较复杂或者数据源较大，此值可能不够。 如果必要，可以大幅增大该值，以便有足够的时间进行处理。 例如，如果将 **“查询超时值”** 设置为 600，则查询可以持续运行 10 分钟之久。  
  
 有关预测查询的详细信息，请参阅 [数据挖掘查询任务和操作指南](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)。  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>配置数据挖掘查询的超时值  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，从 **“工具”** 菜单中选择 **“选项”**。  
  
2.  在 **“选项”** 窗格中，展开 **“商业智能设计器”**。  
  
3.  单击 **“查询超时值”** 文本框，然后键入一个秒数值。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘查询任务和操作指南](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
