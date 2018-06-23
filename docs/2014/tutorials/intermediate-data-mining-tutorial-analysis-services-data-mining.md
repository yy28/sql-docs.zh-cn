---
title: 中间 Data Mining Tutorial (Analysis Services-数据挖掘) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 404b31d5-27f4-4875-bd60-7b2b8613eb1b
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 545c219623331ef167731c3142f36642e530307a
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312295"
---
# <a name="intermediate-data-mining-tutorial-analysis-services---data-mining"></a>数据挖掘中级教程（Analysis Services - 数据挖掘）
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供用于创建和使用数据挖掘模型的集成的环境。 您可以方便地绑定到数据源、针对同一个数据创建和测试多个模型并部署要用于进行预测分析的模型。  
  
 在数据挖掘基础教程中，您学习了如何使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建数据挖掘解决方案，而且生成了三个支持目标邮递活动的模型，这些模型可用来分析客户购买行为并确定潜在的购买目标。  
  
 本中级教程基于这些经验而构建，其中介绍了几个新方案（包括预测和市场篮分析等常见业务要求）。 您将学习如何创建时序模型、关联模型以及顺序分析和聚类分析模型。 最后，您将学习如何使用神经网络了解数据相关性，以及使用逻辑回归进行预测。  
  
 这些课程是相互独立的，可以单独完成。  
  
 若要完成以下教程，你应熟悉与数据挖掘工具和基本的数据挖掘教程中引入的挖掘模型查看器。  
  
 所有的方案都使用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据源，但是您将为不同的方案创建不同的数据源视图。 只要您是首先创建数据源，就可以按任何顺序做练习。  
  
## <a name="lesson-scenarios"></a>课程方案  
 在成功完成目标邮寄活动之后，系统已经要求您利用自己的数据挖掘知识来开发几个要用于进行业务规划的新模型。 其中包括以下任务：  
  
-   **预测：** 将创建*时序*模型中，世界各地的不同区域中的产品的销售量做出预测。 将开发为每个区域的单个模型并了解如何使用*跨预测*。  
  
-   **市场篮分析：** 将创建*关联模型*，若要分析的访问到期间购买产品分组[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]电子商务网站。 基于此市场篮模型，你可以向客户推荐产品。  
  
-   **序列分析：** 生成*聚类分析模型的序列*、 分析顺序客户购买产品的顺序。 您可以基于这个模型规划对网站设计或新产品进行的更改。  
  
-   **重分析：** 你使用*神经网络*模型浏览调用中心数据中的较差的服务质量的可能原因。 根据从初步模型的见解，你将创建*逻辑回归模型*来预测改进客户体验的策略。  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程将讲述如何创建和使用多种类型的数据挖掘算法。 本教程分为以下几课：  
  
 [第 1 课： 创建中级数据挖掘解决方案&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
 在本课中，您将基于 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库创建一个新的项目，以便支持多个新数据源视图和更多的挖掘模型。  
  
 [第 2 课： 生成预测方案&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
 在本课中，您将创建一个可用作预测方案一部分的挖掘模型， 还将浏览用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法生成的挖掘模型。  
  
 您将为每个地区生成单独的模型，而且还生成一个可用于进行交叉预测的通用模型。  
  
 [第 3 课： 生成市场篮方案&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
 在本课中，您将添加一个新的数据源视图，并学习如何处理嵌套表及其键。 您将基于此数据创建一个可用作市场篮方案一部分的挖掘模型。 您还将浏览用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法生成的挖掘模型。  
  
 [第 4 课： 构建群集方案的序列&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
 在本课中，您将创建一个可用作顺序分析和聚类分析方案一部分的挖掘模型， 还将学习如何利用通过 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法生成的挖掘模型。  
  
 [第 5 课： 生成神经网络和逻辑回归模型&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
 在本课中，您将使用 Microsoft 神经网络和 Microsoft 逻辑回归算法创建若干相关的挖掘模型。 您还将学习如何使用数据源视图来基于模型浏览数据。  
  
## <a name="requirements"></a>要求  
 请确保已安装下列软件：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 。  
  
 为了增强安全性，默认情况下将不安装该示例数据库。 若要安装的官方数据库[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请访问[Microsoft SQL 示例数据库](http://go.microsoft.com/fwlink/?LinkId=88417)页，选择示例数据库的适当版本。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Bike Buyer DMX 教程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [市场篮 DMX 教程](../../2014/tutorials/market-basket-dmx-tutorial.md)  
  
  