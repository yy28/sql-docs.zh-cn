---
title: "创建关系挖掘结构 |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- data mining [Analysis Services], structure
- mining structures [Analysis Services], creating
- relational mining models [Analysis Services]
- OLAP mining models [Analysis Services]
ms.assetid: 5547d639-377d-4ca7-88fc-ce1f9e2babc5
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 82fa652f76c1818ef6538b379723e7f91c8482ab
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-relational-mining-structure"></a>创建关系挖掘结构
  大多数数据挖掘模型都基于关系数据源。 创建关系数据挖掘模型的好处是，您可以汇集即席数据并定型和更新模型，此操作不会像创建多维数据集那样复杂。  
  
 关系挖掘结构可从不同源绘制数据。 只要原始数据可定义为数据源视图的一部分，就可以将该数据存储在表、文件或关系数据库系统中。 例如，如果数据位于 Excel、SQL Server 数据仓库或 SQL Server 报表数据库中，或位于通过 OLE DB 或 ODBC 访问接口访问的外部源中，则应使用关系挖掘结构。  
  
 本主题概述了如何使用数据挖掘向导来创建关系挖掘结构。  
  
 [要求](#BKMK_Relational_Structure)  
  
 [创建关系挖掘结构的过程](#BKMK_Relational_Structure)  
  
 [如何选择数据源](#BKMK_ChooseRelData)  
  
 [如何指定内容类型和数据类型](#bkmk_ContentDataType)  
  
 [创建维持数据集的原因和方式](#bkmk_Holdout)  
  
 [启用钻取的原因和方式](#BKMK_DrillThru)  
  
## <a name="requirements"></a>要求  
 首先，您必须具有现有数据源。 如果数据源尚不存在，则可使用数据源设计器设置一个数据源。 有关详细信息，请参阅[创建数据源（SSAS 多维）](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)。  
  
 接下来，请使用数据源视图向导将所需数据汇集到单个数据源视图中。 有关如何使用数据源视图选择、转换、筛选或管理数据的详细信息，请参阅 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
##  <a name="BKMK_Relational_Structure"></a> 过程概述  
 通过在解决方案资源管理器中右键单击“挖掘结构”节点，然后选择“添加新的挖掘结构”来启动数据挖掘向导。 该向导可指导您通过以下步骤创建新关系挖掘模型的结构：  
  
1.  **选择定义方法**：选择数据源类型，然后选择 **“从关系数据库或数据仓库”**。  
  
2.  **创建数据挖掘结构**：确定是仅生成结构还是生成具有挖掘模型的结构。  
  
     也可以为初始模型选择适当的算法。 有关最适合特定任务的算法的指导，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
3.  **选择数据源视图**：选择要用于定型模型的数据源视图。 该数据源视图也可以包含用于测试的数据或不相关的数据。 您可以选择结构和模型中实际使用的数据。 还可以稍后对数据应用筛选器。  
  
4.  **指定表类型**：选择包含用于分析的事例的表。 对于某些数据集（特别是用于生成市场篮模型的数据集），您也可以包含要用作嵌套表的相关表。  
  
     对于每个表，您必须指定相应的键，以便算法了解如何标识唯一记录和相关记录（如果您已添加嵌套表）。  
  
     有关详细信息，请参阅 [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md)。  
  
5.  **指定定型数据**：在此页上，您可以选择包含用于分析的最重要数据的 *事例表*。  
  
     对于某些数据集（特别是用于生成市场篮模型的数据集），您也可以包含相关表。 嵌套表中的值将作为与主表中单个行（或事例）相关的多个值进行处理。  
  
6.  **指定列内容和数据类型**：对于结构中使用的每个列，您必须同时选择 *数据类型* 和 *内容类型*。  
  
     虽然该向导将自动检测可能的数据类型，但您无需使用向导所建议的数据类型。 例如，即使数据包含数字，它们也可能代表类别数据。 将自动为指定为键的列分配该特定模型类型的正确数据类型。 有关详细信息，请参阅[挖掘模型列](../../analysis-services/data-mining/mining-model-columns.md)和[数据类型（数据挖掘）](../../analysis-services/data-mining/data-types-data-mining.md)。  
  
     为模型中使用的每个列选择的 *内容类型* 将告知算法数据的处理方式。  
  
     例如，您可能会决定离散化数字，而不是使用连续值。 您也可以要求算法自动检测列的最佳内容类型。 有关详细信息，请参阅[内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
7.  **创建测试集**：在此页上，您可以告知向导应留出多少数据以便测试模型。 如果数据将支持多个模型，则最好是创建一个保留数据集，以便能基于同一数据测试所有模型。  
  
     有关详细信息，请参阅[测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)。  
  
8.  **完成向导**：在此页上，您可以为新的挖掘结构和关联的挖掘模型提供名称，并保存该结构和模型。  
  
     也可以根据模型类型设置一些重要选项。 例如，可以对该结构启用钻取功能。  
  
     此时，该挖掘结构及其模型仅为元数据；您将需要处理它们以获取结果。  
  
##  <a name="BKMK_ChooseRelData"></a> 如何选择关系数据  
 关系挖掘结构可以基于可通过 OLE DB 数据源获取的任何数据。 如果源数据包含在多个表内，则您可以使用数据源视图将所需的表和列汇集在同一位置。  
  
 如果表包括任何一对多关系（例如，对于您要分析的每个客户，您具有多个采购记录），您可以添加这两个表，然后使用一个表作为事例表并将来自关系的多方的数据作为嵌套表进行链接。  
  
 挖掘结构中的数据是从现有数据源视图中的内容派生而来的。 可以在数据源视图内根据需要修改数据，并添加基础关系数据中可能不会显示的关系或派生列。 您也可以在数据源视图内创建命名计算或聚合。 如果您无法控制数据源中数据的排列方式，或者您需要尝试对数据挖掘模型使用不同的数据聚合，这些功能会很有用。  
  
 您无需使用所有可用数据；可以选择要包含在挖掘结构中的列。 所有基于该结构的模型然后可使用这些列，或者您可以为特定模型将某些列标记为 **Ignore** 。 可以使数据挖掘模型的用户从该挖掘模型的结果进行深化，以查看没有包括在挖掘模型中的其他挖掘结构列。  
  
##  <a name="bkmk_ContentDataType"></a> 如何指定内容类型和数据类型  
 数据类型与在 SQL Server 或其他应用程序接口中指定的数据类型极其相似：日期和时间、不同大小的数字、布尔值、文本及其他离散数据。  
  
 但是，内容数据对数据挖掘非常重要并会影响分析结果。 内容数据将告诉算法应如何处理数据：是应按照连续范围处理数字还是应将数字转换成二进制？ 有多少个可能的值？ 每个值是否都不重复？ 如果值是一个键，那么该键属于哪一种类型 - 它表示日期/时间值、序列还是其他类型的键？  
  
 请注意，数据类型的选择会限制内容类型的选择。 例如，您无法离散化非数字值。 如果您无法查看所需内容类型，则可单击 **“上一步”** 返回到数据类型页，并尝试其他数据类型。  
  
 您无需过多担心内容类型会出错。 只要挖掘结构中的数据类型集支持新的内容类型，就可以很轻松地创建新模型并更改该模型中的内容类型。 为了满足试验需求或其他算法的要求，使用不同的内容类型创建多个模型也是一项很常见的操作。  
  
 例如，如果数据包含一个收入列，则可在使用 Microsoft 决策树算法时创建两个不同的模型，并将该列交替配置为连续数字或离散范围。 但是，如果您添加使用 Microsoft Naïve Bayes 算法的模型，则会强制您仅将该列更改为离散化值，因为该算法不支持连续数字。  
  
##  <a name="bkmk_Holdout"></a> 将数据拆分为定型集和测试集的原因和方式  
 在该向导即将结束时，您必须确定是否将数据分区为定型集和测试集。 用于设置随机抽样的部分数据以进行测试的功能非常方便，因为它确保对与新挖掘结构关联的所有挖掘模型使用一致的测试数据集。  
  
> [!WARNING]  
>  请注意，此选项无法用于所有模型类型。 例如，如果您创建一个预测模型，则将无法使用维持，因为时序算法要求数据中没有空白。 有关支持维持数据集的模型类型的列表，请参阅 [定型数据集和测试数据集](../../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
 若要创建此维持数据集，您需要指定要用于测试的数据的百分比。 所有剩余数据将用于定型。 （可选）您可以设置用于测试的事例的最大数目，或设置用于启动随机选择过程的种子值。  
  
 维持数据集的定义与挖掘结构存储在一起，因此在每次基于该结构创建新模型时，都可以使用该测试数据集来评估模型的准确性。 如果您删除挖掘结构的缓存，则有关用于定型的事例和用于测试的事例的信息也将被删除。  
  
##  <a name="BKMK_DrillThru"></a> 启用钻取的原因和方式  
 在该向导即将结束时，您可以选择启用 *钻取*。 此选项很容易被忽略，但它很重要。 使用钻取功能，可以通过查询挖掘模型来查看挖掘结构中的源数据。  
  
 为何此功能会很有用？ 假设您查看的是聚类分析模型的结果，并希望查看已放入特定分类的客户。 通过使用钻取功能，您可以查看详细信息（例如，联系人信息）。  
  
> [!WARNING]  
>  若要使用钻取功能，您必须在创建挖掘结构时启用它。 以后，您可以通过对模型设置属性来对其启用钻取功能，但挖掘结构要求一开始就设置此选项。 有关详细信息，请参阅[钻取查询（数据挖掘）](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘设计器](../../analysis-services/data-mining/data-mining-designer.md)   
 [数据挖掘向导 &#40;Analysis Services-数据挖掘 &#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)   
 [挖掘模型属性](../../analysis-services/data-mining/mining-model-properties.md)   
 [挖掘结构和结构列的属性](../../analysis-services/data-mining/properties-for-mining-structure-and-structure-columns.md)   
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  

