---
title: 市场篮 DMX 教程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- market basket analysis [Analysis Services]
- tutorials [Data Mining]
- tutorials [DMX]
ms.assetid: 6e262a1d-c89e-4033-8368-46cf25168ef5
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b73a618c5318d88ec6ee09751e09327687d865f4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220577"
---
# <a name="market-basket-dmx-tutorial"></a>市场篮 DMX 教程
  在本教程中，您将学习如何使用数据挖掘扩展插件 (DMX) 查询语言来创建、定型和浏览挖掘模型。 然后，您将使用这些挖掘模型创建预测，说明可能同时购买的产品。  
  
 将使用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 示例数据库中所包含的数据创建挖掘模型，该数据库用于存储虚构公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的数据。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨国制造公司。 公司生产金属和复合材料的自行车，产品远销北美、欧洲和亚洲市场。 公司总部设在华盛顿州的伯瑟尔市，拥有 290 名雇员，而且拥有多个活跃在世界各地的地区性销售团队。  
  
## <a name="tutorial-scenario"></a>教程方案  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 决定创建使用数据挖掘功能的自定义应用程序来预测其客户想要同时购买的产品类型。 该自定义应用程序的目的是能够指定一组产品，并预测另外还有哪些产品将与指定的产品一同购买。 然后，[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 将使用此信息在其网站中添加“建议”功能，并更好地组织向客户提供信息的方式。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供了可用于完成此任务的几个工具：  
  
-   DMX 查询语言  
  
-   [Microsoft 关联算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的查询编辑器  
  
 数据挖掘扩展插件 (DMX) 是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的一种查询语言，可以使用它来创建和处理挖掘模型。 [!INCLUDE[msCoName](../includes/msconame-md.md)]关联算法创建模型，以便预测可能会一起购买的产品。  
  
 本教程的目的是提供将在自定义应用程序中使用的 DMX 查询。  
  
 **有关详细信息：** [数据挖掘解决方案](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>挖掘结构和挖掘模型  
 开始创建 DMX 语句之前，了解 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用来创建挖掘模型的主要对象十分重要。 *挖掘结构*是一种数据结构，它定义从中生成挖掘模型的数据域。 单个挖掘结构可以包含多个*挖掘模型*共享同一个域。 挖掘模型可向挖掘结构所代表的数据应用挖掘模型算法。  
  
 挖掘结构的构造块是挖掘结构列，这些列对数据源所包含的数据进行说明。 这些列包含诸如数据类型、内容类型以及数据分发方式等信息。  
  
 挖掘模型必须包含挖掘结构中所述的键列，以及其余列的子集。 挖掘模型定义每个列的用法以及用于创建挖掘模型的算法。 例如，在 DMX 中，您可以将一列指定为键列或 PREDICT 列。 如果有一列未指定，则会将该列假定为一个输入列。  
  
 在 DMX 中，有两种创建挖掘模型的方式。 您可以使用 `CREATE MINING MODEL` 语句同时创建挖掘结构以及关联的挖掘模型，也可以首先使用 `CREATE MINING STRUCTURE` 语句创建挖掘结构，然后使用 `ALTER STRUCTURE` 语句向结构中添加挖掘模型。 下面将介绍这几种方法。  
  
 `CREATE MINING MODEL`  
 使用此语句可以创建挖掘结构以及关联的同名挖掘模型。 挖掘模型名称后追加有“Structure”，以便与挖掘结构区分开。  
  
 如果要创建包含单一挖掘模型的挖掘结构，则此语句将非常有用。  
  
 有关详细信息，请参阅 [CREATE MINING MODEL (DMX)](/sql/dmx/create-mining-model-dmx)。  
  
 CREATE MINING STRUCTURE  
 使用此语句可创建不带任何模型的新挖掘结构。  
  
 在使用 CREATE MINING STRUCTURE 时，还可以创建一个维持数据集，使用该数据集可测试任何基于相同挖掘结构的模型。  
  
 有关详细信息，请参阅 [CREATE MINING STRUCTURE (DMX)](/sql/dmx/create-mining-structure-dmx)。  
  
 `ALTER MINING STRUCTURE`  
 使用此语句可以向服务器中已存在的挖掘结构中添加挖掘模型。  
  
 由于各种原因，您可能需要在单一挖掘结构中添加多个挖掘模型。 例如，可以使用不同的算法创建多个挖掘模型以判断哪种方法效果最佳。 也可以创建使用相同算法的多个挖掘模型，但将每个挖掘模型中的某个参数设置为不同的值来寻找最佳参数设置。  
  
 有关详细信息，请参阅 [ALTER MINING STRUCTURE &#40;DMX&#41;] ((~/dmx/alter-mining-structure-dmx.md)。  
  
 因为您将创建包含多个挖掘模型的挖掘结构，因此使用本教程中的第二种方法。  
  
 **有关详细信息**  
  
 [数据挖掘扩展插件&#40;DMX&#41;引用](/sql/dmx/data-mining-extensions-dmx-reference)，[了解 DMX Select 语句](/sql/dmx/understanding-the-dmx-select-statement)， [DMX 预测查询的结构和用法](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程分为以下几课：  
  
 [第 1 课：创建市场篮挖掘结构](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)  
 在本课中，您将学习如何使用 `CREATE` 语句创建挖掘结构。  
  
 [第 2 课：向市场篮挖掘结构中添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
 在本课中，您将学习如何使用 `ALTER` 语句向挖掘结构中添加挖掘模型。  
  
 [第 3 课：处理市场篮挖掘结构](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
 在本课程中，您将学习如何使用`INSERT INTO`语句处理挖掘结构及其关联的挖掘模型。  
  
 [第 4 课：执行市场篮预测](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
 在本课中，您将学习如何使用 `PREDICTION JOIN` 语句根据挖掘模型创建预测。  
  
## <a name="requirements"></a>要求  
 执行本教程前，请确保安装了下列各项：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库  
  
 为了增强安全性，默认情况下将不安装该示例数据库。 若要安装的正式示例数据库[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请转到[ http://www.CodePlex.com/MSFTDBProdSamples ](http://go.microsoft.com/fwlink/?LinkId=88417)或在 Microsoft SQL Server 示例和社区项目主页上，以在 Microsoft SQL Server 产品示例部分。 单击**数据库**，然后单击**版本**选项卡上，选择所需的数据库。  
  
> [!NOTE]  
>  在阅读教程时，我们建议您将添加**下一主题**并**上一个主题**到文档查看器工具栏按钮。  
  
## <a name="see-also"></a>请参阅  
 [自行车购买者 DMX 教程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [第 3 课： 生成市场篮方案&#40;数据挖掘中级教程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
