---
title: 数据挖掘中级教程（Analysis Services 数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 404b31d5-27f4-4875-bd60-7b2b8613eb1b
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4c244701d8a58765061ef3bde1f918c8be5a941d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63017180"
---
# <a name="intermediate-data-mining-tutorial-analysis-services---data-mining"></a>数据挖掘中级教程（Analysis Services - 数据挖掘）
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供用于创建和使用数据挖掘模型的集成环境。 您可以方便地绑定到数据源、针对同一个数据创建和测试多个模型并部署要用于进行预测分析的模型。  
  
 在数据挖掘基础教程中，您学习了如何使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建数据挖掘解决方案，而且生成了三个支持目标邮递活动的模型，这些模型可用来分析客户购买行为并确定潜在的购买目标。  
  
 本中级教程基于这些经验而构建，其中介绍了几个新方案（包括预测和市场篮分析等常见业务要求）。 您将学习如何创建时序模型、关联模型以及顺序分析和聚类分析模型。 最后，您将学习如何使用神经网络了解数据相关性，以及使用逻辑回归进行预测。  
  
 这些课程是相互独立的，可以单独完成。  
  
 若要完成以下教程，您应该熟悉数据挖掘工具，以及在数据挖掘基础教程中引入的挖掘模型查看器。  
  
 所有的方案都使用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据源，但是您将为不同的方案创建不同的数据源视图。 只要您是首先创建数据源，就可以按任何顺序做练习。  
  
## <a name="lesson-scenarios"></a>课程方案  
 在成功完成目标邮寄活动之后，系统已经要求您利用自己的数据挖掘知识来开发几个要用于进行业务规划的新模型。 其中包括以下任务：  
  
-   **预测：** 您将创建*时序*模型，以预测世界各地不同地区的产品销售额。 您将为每个区域开发单独的模型，并学习如何使用*交叉预测*。  
  
-   **市场篮分析：** 您将创建一个*关联模型*，用于分析在访问[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]电子商务网站时所购买产品的分组。 根据此市场篮模型，你可以向客户推荐产品。  
  
-   **序列分析：** 你构建了*顺序分析和聚类分析模型*，用于分析客户购买产品的顺序。 您可以基于这个模型规划对网站设计或新产品套餐进行的更改。  
  
-   **因素分析：** 您可以使用*神经网络*模型来浏览呼叫中心数据中服务质量差的可能原因。 基于初步模式的见解，你将创建*逻辑回归模型*来预测改善客户体验的策略。  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程将讲述如何创建和使用多种类型的数据挖掘算法。 本教程分为以下几课：  
  
 [第1课：创建中级数据挖掘解决方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
 在本课中，您将基于 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库创建一个新的项目，以便支持多个新数据源视图和更多的挖掘模型。  
  
 [第2课： &#40;中级数据挖掘教程构建预测方案&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
 在本课中，您将创建一个可用作预测方案一部分的挖掘模型， 还将浏览用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法生成的挖掘模型。  
  
 您将为每个地区生成单独的模型，而且还生成一个可用于进行交叉预测的通用模型。  
  
 [第3课：生成市场篮方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
 在本课中，您将添加一个新的数据源视图，并学习如何处理嵌套表及其键。 您将基于此数据创建一个可用作市场篮方案一部分的挖掘模型。 您还将浏览用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法生成的挖掘模型。  
  
 [第4课：生成顺序分析和聚类分析方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
 在本课中，您将创建一个可用作顺序分析和聚类分析方案一部分的挖掘模型， 还将学习如何利用通过 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法生成的挖掘模型。  
  
 [第5课：生成神经网络和逻辑回归模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
 在本课中，您将使用 Microsoft 神经网络和 Microsoft 逻辑回归算法创建若干相关的挖掘模型。 您还将学习如何使用数据源视图来基于模型浏览数据。  
  
## <a name="requirements"></a>要求  
 请确保已安装下列软件：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]带有[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据库的。  
  
 为了增强安全性，默认情况下将不安装该示例数据库。 若要安装的正式数据库[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请访问[Microsoft SQL 示例数据库](https://go.microsoft.com/fwlink/?LinkId=88417)页，并选择相应的示例数据库版本。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [自行车购买者 DMX 教程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [市场篮 DMX 教程](../../2014/tutorials/market-basket-dmx-tutorial.md)  
  
  
