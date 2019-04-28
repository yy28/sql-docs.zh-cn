---
title: 创建挖掘结构 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea04b08f98385755f006c1a67125a87dc71e41f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62854343"
---
# <a name="create-mining-structure-dmx"></a>CREATE MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在数据库中创建新的挖掘结构，并根据需要定义定型和测试分区。 创建挖掘结构后，可以使用[ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md)语句将模型添加到挖掘结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE [SESSION] MINING STRUCTURE <structure>  
(  
    [(<column definition list>)]  
)  
[WITH HOLDOUT (<holdout-specifier> [OR <holdout-specifier>])]  
[REPEATABLE(<holdout seed>)]  
<holdout-specifier>::=  <holdout-maxpercent> PERCENT | <holdout-maxcases> CASES  
```  
  
## <a name="arguments"></a>参数  
 *structure*  
 结构的唯一名称。  
  
 *列定义列表*  
 列定义的逗号分隔列表。  
  
 *holdout-maxpercent*  
 一个介于 1 和 100 之间的整数，指示要留作测试的数据所占的百分比。  
  
 *holdout-maxcases*  
 一个整数，指示要用于测试的最大事例数。  
  
 如果指定的最大事例值大于输入事例数，则所有输入事例都将用于测试并且会引发警告。  
  
> [!NOTE]  
>  如果既指定了事例百分比，又指定了最大事例数，则采用这两个限制中较小的一个。  
  
 *维持种子*  
 一个整数，用作启动分区数据的种子。  
  
 如果设置为 0，则挖掘结构 ID 的哈希将用作种子。  
  
> [!NOTE]  
>  如果需要确保分区能够重新生成，则应指定种子。  
  
 默认值：REPEATABLE （0)  
  
## <a name="remarks"></a>备注  
 通过指定列的列表可以定义挖掘结构；如果需要，还可以指定列之间的层次结构关系，然后再根据需要将挖掘结构分为定型数据集和测试数据集。  
  
 可选的 SESSION 关键字指示该结构是一个只能在当前会话持续期间使用的临时结构。 会话终止时，该结构以及基于该结构的所有模型都将被删除。 若要创建临时挖掘结构和模型，必须首先设置数据库属性，AllowSessionMiningModels。 有关详细信息，请参阅 [Data Mining Properties](../analysis-services/server-properties/data-mining-properties.md)。  
  
## <a name="column-definition-list"></a>列定义列表  
 定义挖掘结构时，在列定义列表中包括每个列的下列信息：  
  
-   名称（必选）  
  
-   日期类型（必需）  
  
-   Distribution  
  
-   建模标志列表  
  
-   内容类型（必需）  
  
-   与属性列的关系（仅在适用时为必需），由 RELATED TO 子句指示  
  
 使用以下列定义列表语法来定义单个列：  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<column relationship>]  
```  
  
 使用以下列定义列表语法来定义嵌套表列：  
  
```  
<column name>    TABLE    ( <column definition list> )  
```  
  
 有关可用于定义结构列的数据类型、内容类型、列分布和建模标志的列表，请参阅下列主题：  
  
-   [数据类型（数据挖掘）](../analysis-services/data-mining/data-types-data-mining.md)  
  
-   [内容类型（数据挖掘）](../analysis-services/data-mining/content-types-data-mining.md)  
  
-   [列分布（数据挖掘）](../analysis-services/data-mining/column-distributions-data-mining.md)  
  
-   [建模标志（数据挖掘）](../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
 可以为一个列定义多个建模标志值。 但是，一个列只能有一个内容类型和数据类型。  
  
### <a name="column-relationships"></a>列关系  
 您可以向任何列定义语句中添加子句，以说明两个列之间的关系。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持以下使用\<列关系 > 子句。  
  
 **与相关**  
 指示值的层次结构。 RELATED TO 列的目标可以是嵌套表的键列、事例行中具有离散值的列或另一个包含 RELATED TO 子句并指示更深层次结构的列。  
  
## <a name="holdout-parameters"></a>维持参数  
 指定维持参数时，结构数据分区也将随即创建。 为维持指定的数据量用于测试，其余数据用于定型。 默认情况下，如果使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建挖掘结构，则创建的维持分区包含 30% 的测试数据和 70% 的定型数据。 有关详细信息，请参阅 [Training and Testing Data Sets](../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
 如果使用数据挖掘扩展插件 (DMX) 创建挖掘结构，则必须手动指定要创建维持分区。  
  
> [!NOTE]  
>  **ALTER MINING STRUCTURE**语句不支持维持。  
  
 您最多可以指定三个维持参数。 如果同时指定维持事例和维持百分比的最大数，则将保留事例百分比，直到达到最大事例限制。 作为一个整数后, 跟指定维持百分比**百分比**关键字，并指定事例的最大数目为一个整数后, 跟**情况下**关键字。 您可以按照任何顺序组合这些条件，如下面的示例所示：  
  
```  
WITH HOLDOUT (20 PERCENT)   
WITH HOLDOUT (2000 CASES)   
WITH HOLDOUT (20 PERCENT OR 2000 CASES)   
WITH HOLDOUT (2000 CASES OR 20 PERCENT)  
```  
  
 维持种子控制随机将事例分配给定型数据集或测试数据集这一过程的起点。 通过设置维持种子，可以确保该分区可重复执行。 如果没有指定维持种子，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用挖掘结构的名称来创建种子。 如果重命名结构，则种子值会更改。 维持种子参数可以与一个或多个其他维持参数一起使用。  
  
> [!NOTE]  
>  由于分区信息缓存的定型数据，因此若要使用维持数据，您必须确保**CacheMode**挖掘结构的属性设置为**KeepTrainingData**。 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中，新的挖掘结构的默认设置即是如此。 更改**CacheMode**属性设置为**ClearTrainingCases**上现有的挖掘结构的包含维持分区不会影响任何已处理的挖掘模型。 但是，如果<xref:Microsoft.AnalysisServices.MiningStructureCacheMode>未设置为**KeepTrainingData**，维持参数会产生任何效果。 这意味着所有源数据都用于定型而没有提供测试集。 分区定义是使用结构进行缓存的；如果清理了定型事例的缓存，则同时将清理测试数据的缓存以及维持集的定义。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何使用 DMX 创建包含维持的挖掘结构。  
  
### <a name="example-1-adding-a-structure-with-no-training-set"></a>示例 1：添加不含定型集的结构  
 下面的示例创建新的名为 `New Mailing` 的挖掘结构，并且不创建任何关联的挖掘模型，也不使用维持。 若要了解如何向结构添加挖掘模型，请参阅[ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md)。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)  
```  
  
### <a name="example-2-specifying-holdout-percentage-and-seed"></a>示例 2：指定维持百分比和种子  
 下面的子句可以添加到列定义列表后面，以便定义可用来测试与该挖掘结构关联的所有挖掘模型的数据集。 该语句将创建占全部输入事例的 25% 的测试集，并且不限制最大事例数。 将 5000 用作创建分区的种子。 指定种子后，只要基础数据不变，在您每次处理挖掘结构时，都将选择相同的事例用于测试集。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT) REPEATABLE(5000)  
```  
  
### <a name="example-3-specifying-holdout-percentage-and-max-cases"></a>示例 3:指定维持百分比和最大事例数  
 下面的子句将创建一个测试集，其中包含全部输入事例的 25% 或 2000 个事例（以二者中少者计）。 因为 0 被指定为种子，所以使用挖掘结构的名称来创建种子以开始输入事例抽样。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT OR 2000 CASES) REPEATABLE(0)  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
