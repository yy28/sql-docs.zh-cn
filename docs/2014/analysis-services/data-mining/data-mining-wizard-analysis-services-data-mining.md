---
title: 数据挖掘向导（Analysis Services 数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- OLAP [Analysis Services], mining models
- Data Mining Wizard
- relational mining models [Analysis Services]
ms.assetid: d5fea90f-5f38-4639-8851-7707f6606a12
author: minewiskan
ms.author: owend
ms.openlocfilehash: c0fb91b5343bd6f45eaadb93f71a73b85cb7f3a1
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522743"
---
# <a name="data-mining-wizard-analysis-services---data-mining"></a>数据挖掘向导（Analysis Services - 数据挖掘）
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 每次向数据挖掘项目中添加新的挖掘结构时，都会启动中的数据挖掘向导。 该向导可帮助您选择数据源并设置可定义要用于分析的数据的数据源视图，然后帮助您创建初始模型。  
  
 在该向导的最后阶段，您可以选择将数据划分为定型集和测试集，并启用钻取等功能。  
  
## <a name="what-to-know-before-you-start"></a>开始之前要了解的内容  
 启动向导之前需要了解以下内容。  
  
-   是从关系数据库还是根据 OLAP 数据库中的现有多维数据集生成数据挖掘结构和模型？  
  
-   哪些列包含唯一标识事例记录的键？  
  
-   您要将哪些列或属性用于预测？ 哪些列或属性适合用作分析的输入？  
  
-   应使用哪种算法？ 中提供的算法都 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 具有不同的特征并产生不同的结果。 幸运的是，您并不是只能对每个数据集使用一个模型，您可以通过添加不同的模型来进行任意尝试。  
  
-   您是否需要能针对统一数据集来测试模型？ 如果需要，请考虑使用为测试保留一些数据的选项。 您可以选择一个百分比，并根据需要用指定行数设置其上限。  
  
##  <a name="starting-the-data-mining-wizard"></a><a name="BKMK_Using_DM_Wizard"></a> 启动数据挖掘向导  
 若要使用数据挖掘向导，则必须已在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中打开至少包含一个数据挖掘或 OLAP 项目的解决方案。  
  
-   如果你的解决方案已做好数据挖掘准备，则只需在解决方案资源管理器中右键单击“挖掘结构”**** 节点并选择“新建挖掘结构”**** 即可启动该向导。  
  
-   如果解决方案中未包含任何现有项目，则可添加新的数据挖掘项目。 从“文件”**** 菜单，选择“新建”****，然后选择“项目”****。 确保选择模板 **“Analysis Services 多维和数据挖掘项目”**。  
  
-   您还可以使用 Analysis Services 导入向导从现有数据挖掘解决方案获取元数据。 但是，您不能选择单个对象进行导入；将导入整个数据库，包括任何多维数据集、数据源视图等。另请注意，通过导入创建的新解决方案将自动配置为使用本地默认数据库。 您可能需要先将此更改为其他实例，然后才能处理或浏览对象，如果要从早期版本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]导入，则可能需要更新对访问接口的引用。  
  
 接下来，您将创建挖掘结构和一个关联的数据挖掘模型。 您也可以只创建挖掘结构并在稍后添加模型，但先创建测试模型通常最为轻松。  
  
###  <a name="relational-vs-olap-mining-models"></a><a name="BKMK_Relational"></a> 关系与OLAP 挖掘模型  
 为您提供的下一个重要选项可让您确定是使用关系数据源还是使模型基于多维 (OLAP) 数据。  
  
 此时，数据挖掘向导分为两个路径，具体取决于您的数据源是关系数据源还是位于多维数据集中。 除数据选择进程之外的其他所有内容都是相同的算法选择、添加维持数据集的能力等，但选择多维数据集数据比使用关系数据稍微复杂一些。 （如果您基于多维数据集创建模型，则在最后还会获得一些其他选项。）  
  
 有关每个选项的演练的详细说明，请参阅下列主题：  
  
 [创建关系挖掘结构](create-a-relational-mining-structure.md)  
 引导您完成在生成关系数据挖掘模型时做出的决定。  
  
 [创建 OLAP 挖掘结构](create-an-olap-mining-structure.md)  
 介绍从 OLAP 多维数据集中选择数据时要做出的其他选择。  
  
> [!NOTE]  
>  无需拥有多维数据集或 OLAP 数据库即可进行数据挖掘。 除非数据已存储在多维数据集中，或者要挖掘 OLAP 维度或 OLAP 聚合或计算的结果，否则，我们建议您将关系表或数据源用于数据挖掘。  
  
### <a name="choosing-an-algorithm"></a>选择算法  
 接下来，您必须决定处理数据时要使用的算法。 此决定可能很难做出。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中提供的每种算法都有不同的功能并会产生不同的结果，因此，在确定最适合您的数据和业务问题的模型之前，您可以试用多种不同的模型。 请参阅以下主题以查看每种算法最适合的任务的说明：  
  
 [数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)  
  
 同样，可以使用不同的算法创建多个模型，也可以更改算法的参数来创建不同的模型。 您不应局限于所选的算法，最好的方法是对同一数据创建几个不同的模型。  
  
### <a name="define-the-data-used-for-modeling"></a>定义用于建模的数据  
 除了从源选择数据之外，还必须指定数据源视图中包含 *事例数据*的表。 事例表将用于为数据挖掘模型定型，因此应包含要分析的实体，例如客户及其人口统计信息。 每个事例都必须唯一，且必须能被 *事例键*识别。  
  
 除了指定事例表之外，您还可以将 *嵌套表* 包含在数据中。 嵌套表通常包含有关事例表中实体的附加信息，如客户执行的交易或与实体具有多对一关系的属性。 例如，与 **Customers** 事例表联接的嵌套表可能包括每个客户所购买产品的列表。 在用于分析网站流量的模型中，嵌套表可能包含用户访问过的页面的顺序。 有关详细信息，请参阅[嵌套表（Analysis Services - 数据挖掘）](nested-tables-analysis-services-data-mining.md)  
  
### <a name="additional-features"></a>其他功能  
 为了帮助您选择正确的数据和正确配置数据源，数据挖掘向导还提供了以下功能：  
  
-   **自动检测数据类型**：该向导将检查列值的唯一性和分布情况，然后提供建议的最佳数据类型和数据使用类型。 您可以从列表中选择值来覆盖这些建议。  
  
-   **变量建议**：您可以单击对话框并启动用于计算模型中包含的各个列之间的关联的分析器，并确定在当前给定模型配置的情况下，是否有任何列可能成为结果属性的预测器。 您可以通过键入其他值来覆盖这些建议。  
  
-   **功能选择**：大多数算法都将自动检测作为良好的预测器的列并优先使用这些列。 在包含的值过多的列中，将应用 *功能选择* 来减少数据的基数并增大找到有用模式的机会。 您可以使用模型参数来影响功能选择行为。  
  
-   **自动多维数据集切片**：如果挖掘模型基于 OLAP 数据源，则会自动提供使用多维数据集属性对模型进行切片的功能。 这对于创建基于多维数据集数据子集的模型很适用。  
  
### <a name="completing-the-wizard"></a>完成向导  
 向导中的最后一步是对挖掘结构和关联的挖掘模型进行命名。 根据创建的模型类型，您还具有以下重要选项：  
  
-   如果选择 **“允许钻取”**，则会在模型中启用 *钻取* 。 利用钻取，具有相应权限的用户可以浏览用于生成模型的源数据。  
  
-   如果要生成 OLAP 模型，您可以选择 **“创建新数据挖掘多维数据集”** 或 **“创建数据挖掘维度”** 选项。 可利用这两个选项更轻松地浏览已完成的模型并钻取到基础数据。  
  
 完成数据挖掘向导后，使用数据挖掘设计器来修改挖掘结构和模型、查看模型的准确性、查看结构和模型的特征或者使用模型进行预测。  
  
 [返回页首](#BKMK_Using_DM_Wizard)  
  
## <a name="related-content"></a>相关内容  
 若要了解有关在创建数据挖掘模型时需做出的决策的详细信息，请参阅以下链接：  
  
 [数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)  
  
 [内容类型（数据挖掘）](content-types-data-mining.md)  
  
 [数据类型（数据挖掘）](data-types-data-mining.md)  
  
 [功能选择（数据挖掘）](feature-selection-data-mining.md)  
  
 [缺失值（Analysis Services - 数据挖掘）](missing-values-analysis-services-data-mining.md)  
  
 [对挖掘模型的钻取功能](drillthrough-on-mining-models.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘工具](data-mining-tools.md)   
 [数据挖掘解决方案](data-mining-solutions.md)  
  
  
