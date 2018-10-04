---
title: 定型和测试数据集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- testing mining models
- holdout [data mining]
- testing data mining models
- accuracy testing [data mining]
ms.assetid: 5798fa48-ef3c-4e97-a17c-38274970fccd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9d6c44c63236a351a69b38ef66f14141441c61f7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120259"
---
# <a name="training-and-testing-data-sets"></a>定型数据集和测试数据集
  将数据分为定型集和测试集是评估数据挖掘模型的一个重要部分。 将数据集分为定型集和测试集时，通常大部分数据用于定型，小部分数据用于测试。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会随机地进行数据抽样，以帮助确保测试集和定型集相似。 通过使用相似的数据来进行定型和测试，可以最小化数据差异所造成的影响并更好地了解模型的特征。  
  
 使用定型集处理模型后，可通过对测试集进行预测来测试该模型。 由于测试集内的数据已经包含要预测属性的已知值，因此可以方便地确定模型的预测准确性。  
  
## <a name="creating-test-and-training-sets-for-data-mining-structures"></a>为数据挖掘结构创建测试集和定型集  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，可以在挖掘结构级别对原始数据集进行拆分。 有关定型数据集和测试数据集的大小以及哪个行属于哪个数据集的信息随挖掘结构一起存储，而且所有基于该结构的模型都将这些集用于定型和测试。  
  
 您可以按以下方式针对挖掘结构定义测试数据集：  
  
-   在创建挖掘结构时，使用数据挖掘向导对挖掘结构进行拆分。  
  
-   在数据挖掘设计器的 **“挖掘结构”** 选项卡中修改结构属性。  
  
-   使用分析管理对象 (AMO) 或 XML 数据定义语言 (DDL) 以编程方式创建和修改结构。  
  
### <a name="using-the-data-mining-wizard-to-divide-a-mining-structure"></a>使用数据挖掘向导对挖掘结构进行拆分  
 默认情况下，在为挖掘结构定义了数据源之后，数据挖掘向导会将数据拆分成两个集：70% 的源数据用于定型模型，30% 的源数据用于测试模型。 这是选择的默认值，因为在数据挖掘中通常使用 70-30 这一比率，但是，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，可以根据自己的需求更改此比率。  
  
 您还可以配置该向导以设置定型事例的最大数量，也可以组合不同的限制来允许事例的最大百分比达到所指定的最大事例数。 如果您既指定了事例的最大百分比又指定了事例的最大数量， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会将这两个限制的较小者用作测试集的大小。 例如，如果指定测试事例维持在 30% 的比率，测试事例的最大数量为 1000，则测试集的大小决不会超过 1000 个事例。 如果您想确保测试集的大小保持一致（即使向模型中添加更多的定型数据也是如此），则这可能非常有用。  
  
 如果您在不同的挖掘结构中使用相同的数据源视图，并希望以大体相同的方式对所有挖掘结构及其模型中的数据进行拆分，则应当指定用来初始化随机抽样的种子。 指定的值时`HoldoutSeed`，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]将使用该值来开始抽样。 否则，抽样功能将根据挖掘结构的名称使用哈希算法来创建种子值。  
  
> [!NOTE]  
>  如果您使用 `EXPORT` 和 `IMPORT` 语句来创建挖掘结构的副本，则新挖掘结构将具有相同的定型数据集和测试数据集，因为导出过程将创建新 ID，但是使用相同的名称。 不过，如果两个挖掘结构使用相同的基础数据源但是具有不同的名称，那么，为每个挖掘结构创建的集将有所不同。  
  
### <a name="modifying-structure-properties-to-create-a-test-data-set"></a>修改结构属性以创建测试数据集  
 如果您在创建和处理挖掘结构之后又决定取消一个测试数据集，可以修改挖掘结构的属性。 若要更改数据的分区方式，请编辑下列属性：  
  
|“属性”|Description|  
|--------------|-----------------|  
|`HoldoutMaxCases`|指定要包括在测试集内的最大事例数。|  
|`HoldoutMaxPercent`|指定测试集内要包括的事例数在整个数据集中所占的百分比。 如果没有数据集，则将指定 0。|  
|`HoldoutSeed`|指定为分区随机选择数据时要用作种子的整数值。 此值不影响定型集内的事例数，而是将确保分区能够重复。|  
  
 如果您在现有的结构中添加或更改测试数据集，必须重新处理该结构以及所有的关联模型。 此外，由于拆分源数据会导致针对数据的另一个子集为模型定型，因此您可能会在模型中看到不同的结果。  
  
### <a name="specifying-holdout-programmatically"></a>以编程方式指定维持  
 您可以使用 DMX 语句、AMO 或 XML DDL 来定义挖掘结构的测试数据集和定型数据集。 ALTER MINING STRUCTURE 语句不支持使用维持参数。  
  
-   **DMX** 在数据挖掘扩展插件 (DMX) 语言中，CREATE MINING STRUCTURE 语句已扩展为包括 WITH HOLDOUT 子句。  
  
-   **ASSL** 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 可以创建新的挖掘结构或向现有挖掘结构添加测试数据集。  
  
-   **AMO** 还可以使用 AMO 来查看和修改维持数据集。  
  
 可以通过查询数据挖掘架构行集来查看有关现有挖掘结构中维持数据集的信息。 可以通过发出 DISCOVER ROWSET 调用或者使用 DMX 查询，来查看此信息。  
  
## <a name="retrieving-information-about-holdout-data"></a>检索有关维持数据的信息  
 默认情况下，有关定型数据集和测试数据集的所有信息都会进行缓存，以便您可以使用现有数据为新模型定型，然后进行测试。 还可以定义要应用于所缓存的维持数据的筛选器，以便可以针对数据的子集评估模型。  
  
 事例分为定型数据集和测试数据集的方式取决于您配置维持的方式和所提供的数据。 如果要确定用于定型或测试的事例数，或查找有关定型集和测试集内所包括事例的其他详细信息，可以通过创建 DMX 查询来查询模型结构。 例如，下面的查询将返回模型的定型集内所使用的事例。  
  
```  
SELECT * from <structure>.CASES WHERE IsTrainingCase()  
```  
  
 若要仅检索测试事例，并针对挖掘结构中的某一列筛选测试事例，请使用下面的语法：  
  
```  
SELECT * from <structure>.CASES WHERE IsTestCase() AND <structure column name> = '<value>'  
```  
  
## <a name="limitations-on-the-use-of-holdout-data"></a>维持数据的使用限制  
  
-   若要使用维持参数，必须将挖掘结构的 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性设置为默认值（即 `KeepTrainingCases`）。 如果您更改`CacheMode`属性设置为`ClearAfterProcessing`，然后重新处理挖掘结构，则分区将丢失。  
  
-   不能从时序模型删除数据；因此不能将源数据分为定型集和测试集。 如果开始创建挖掘结构和模型并选择 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法，将禁用创建维持数据集的选项。 如果挖掘结构的事例级别或嵌套表级别中包含 KEY TIME 列，也将禁止使用维持数据。  
  
-   可能因为疏忽这样配置维持数据集：将整个数据集用于测试，没有为定型保留数据。 但是，如果这样做， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会引发错误，以便您可以解决此问题。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也会向您发出警告。  
  
-   在多数情况下，默认的维持值 (30) 会在定型数据和测试数据之间提供良好的平衡。 不能通过任何一种简单的方法来确定数据集应当多大才能提供足够的定型，或者如何可使定型集稀疏并且仍可以避免过度拟合。 不过，在生成模型后，可以使用交叉验证来评估特定模型的数据集。  
  
-   除了上表中列出的属性以外，AMO 和 XML DDL 中还提供了一个只读属性：`HoldoutActualSize`。 但是，因为分区的实际大小不能确定准确地直到处理该结构后，您应检查之前检索的值是否已处理模型`HoldoutActualSize`属性。  
  
## <a name="related-content"></a>相关内容  
  
|主题|链接|  
|------------|-----------|  
|说明模型的筛选器如何与定型数据集和测试数据集进行交互。|[挖掘模型的筛选器&#40;Analysis Services-数据挖掘&#41;](mining-models-analysis-services-data-mining.md)|  
|说明定型数据和测试数据的使用如何影响交叉验证。|[交叉验证&#40;Analysis Services-数据挖掘&#41;](cross-validation-analysis-services-data-mining.md)|  
|提供用于处理挖掘结构中定型集和测试集的编程接口的相关信息。|[AMO 概念和对象模型](../multidimensional-models/analysis-management-objects/amo-concepts-and-object-model.md)<br /><br /> [MiningStructure 元素&#40;ASSL&#41;](../scripting/objects/miningstructure-element-assl.md)|  
|提供用于创建维持集的 DMX 语法。|[创建挖掘结构&AMP;#40;DMX&AMP;#41;](/sql/dmx/create-mining-structure-dmx)|  
|在定型集和测试集中检索有关事例的信息。|[数据挖掘架构行集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)<br /><br /> [查询数据挖掘架构行集&#40;Analysis Services-数据挖掘&#41;](data-mining-schema-rowsets-ssas.md)|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘工具](data-mining-tools.md)   
 [数据挖掘概念](data-mining-concepts.md)   
 [数据挖掘解决方案](data-mining-solutions.md)   
 [测试和验证&#40;数据挖掘&#41;](testing-and-validation-data-mining.md)  
  
  
