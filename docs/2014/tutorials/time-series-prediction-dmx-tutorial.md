---
title: 时间序列预测 DMX 教程 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2a9e3e5db1e0f21bfe3822d73fd0e3c0b456e250
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312184"
---
# <a name="time-series-prediction-dmx-tutorial"></a>时序预测 DMX 教程
  在本教程中，将学习如何创建时序挖掘结构，创建三个自定义时序挖掘模型，然后使用这些模型进行预测。  
  
 挖掘模型基于 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 示例数据库（存储虚构公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的数据）中所包含的数据。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨国制造公司。  
  
## <a name="tutorial-scenario"></a>教程方案  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 已经决定使用数据挖掘功能来生成销售预测。 它们已生成了某些区域的预测模型;有关详细信息，请参阅[第 2 课： 生成预测方案&#40;中间 Data Mining Tutorial&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。 但是，销售部门需要能够定期用新的销售数据更新数据挖掘模型。 它们还希望自定义模型来提供不同的预测。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供了一些可以用来完成此任务的工具：  
  
-   数据挖掘扩展插件 (DMX) 查询语言  
  
-   Microsoft 时序算法  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的查询编辑器  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法创建可用于预测时间相关数据的模型。 数据挖掘扩展插件 (DMX) 是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的一种查询语言，可用来创建挖掘模型和预测查询。  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程假定您已经熟悉 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用来创建挖掘模型的对象。 如果你以前没有创建挖掘结构或挖掘模型使用 DMX，请参阅[Bike Buyer DMX 教程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)。  
  
 本教程分为以下几课：  
  
 [第 1 课：创建时序挖掘模型和挖掘结构](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 在本课中，您将学习如何使用 `CREATE MINING MODEL` 语句添加新的预测模型及其相关的挖掘模型。  
  
 [第 2 课：向时序挖掘结构添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
 在本课中，您将学习如何使用 ALTER MINING STRUCTURE 语句向时序结构中添加新的挖掘模型。 您还将学习如何自定义用来分析时序的算法。  
  
 [第 3 课：准备时序结构和模型](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
 在本课中，您将学习如何使用 `INSERT INTO` 语句并用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库中的数据填充结构来为模型定型。  
  
 [第 4 课：使用 DMX 创建时序预测](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
 在本课中，您将学习如何创建时序预测。  
  
 [第 5 课：扩展时序模型](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
 在本课中，您将学习在进行预测时，如何使用 `EXTEND_MODEL_CASES` 参数用新数据更新模型。  
  
## <a name="requirements"></a>要求  
 执行本教程前，请确保安装了下列各项：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库  
  
 为了增强安全性，默认情况下将不安装该示例数据库。 若要安装的官方示例数据库[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请转到[ http://www.CodePlex.com/MSFTDBProdSamples ](http://go.microsoft.com/fwlink/?LinkId=88417)或在 Microsoft SQL Server 示例和社区项目主页上，以在 Microsoft SQL Server 产品示例部分。 单击**数据库**，然后单击**版本**选项卡并选择所需的数据库。  
  
> [!NOTE]  
>  当你查看教程时，我们建议你添加**下一主题**和**上一步主题**到文档查看器工具栏按钮。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中间数据挖掘教程&#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  