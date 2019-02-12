---
title: 时间时序预测 DMX 教程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1623f824c062c270268323fd45ebf0e9533c8788
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010798"
---
# <a name="time-series-prediction-dmx-tutorial"></a>时序预测 DMX 教程
  在本教程中，将学习如何创建时序挖掘结构，创建三个自定义时序挖掘模型，然后使用这些模型进行预测。  
  
 挖掘模型基于 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 示例数据库（存储虚构公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的数据）中所包含的数据。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨国制造公司。  
  
## <a name="tutorial-scenario"></a>教程方案  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 已经决定使用数据挖掘功能来生成销售预测。 他们已构建的某些地区的预测模型;有关详细信息，请参阅[第 2 课：生成预测方案&#40;数据挖掘中级教程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。 但是，销售部门需要能够定期用新的销售数据更新数据挖掘模型。 它们还希望自定义模型来提供不同的预测。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供了可用于完成此任务的几个工具：  
  
-   数据挖掘扩展插件 (DMX) 查询语言  
  
-   Microsoft 时序算法  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的查询编辑器  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法创建可用于预测时间相关数据的模型。 数据挖掘扩展插件 (DMX) 是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的一种查询语言，可用来创建挖掘模型和预测查询。  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程假定您已经熟悉 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用来创建挖掘模型的对象。 如果您不之前已创建挖掘结构或挖掘模型使用 DMX，请参阅[自行车购买者 DMX 教程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)。  
  
 本教程分为以下几课：  
  
 [第 1 课：创建时序挖掘模型和挖掘结构](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 在本课中，您将学习如何使用 `CREATE MINING MODEL` 语句添加新的预测模型及其相关的挖掘模型。  
  
 [第 2 课：向时序挖掘结构添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
 在本课中，您将学习如何使用 ALTER MINING STRUCTURE 语句向时序结构中添加新的挖掘模型。 您还将学习如何自定义用来分析时序的算法。  
  
 [第 3 课：处理时序结构和模型](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
 在本课中，您将学习如何使用 `INSERT INTO` 语句并用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库中的数据填充结构来为模型定型。  
  
 [第 4 课：创建时序预测使用 DMX](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
 在本课中，您将学习如何创建时序预测。  
  
 [第 5 课：扩展时序模型](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
 在本课中，您将学习在进行预测时，如何使用 `EXTEND_MODEL_CASES` 参数用新数据更新模型。  
  
## <a name="requirements"></a>要求  
 执行本教程前，请确保安装了下列各项：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库  
  
 为了增强安全性，默认情况下将不安装该示例数据库。 若要安装的正式示例数据库[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请转到[ http://www.CodePlex.com/MSFTDBProdSamples ](https://go.microsoft.com/fwlink/?LinkId=88417)或在 Microsoft SQL Server 示例和社区项目主页上，以在 Microsoft SQL Server 产品示例部分。 单击**数据库**，然后单击**版本**选项卡上，选择所需的数据库。  
  
> [!NOTE]  
>  在阅读教程时，我们建议您将添加**下一主题**并**上一个主题**到文档查看器工具栏按钮。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [数据挖掘中级教程&#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
