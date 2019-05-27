---
title: 预测查询 （数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e5e6686c-1360-480e-8c0d-8a56204fbed9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a1026597a0ae000b91e088d2457b3c9dd607044b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083119"
---
# <a name="prediction-queries-data-mining"></a>预测查询（数据挖掘）
  典型数据挖掘项目的目标是使用挖掘模型来进行预测。 例如，您可能希望预测某个服务器群集的预期停机时间量，或者生成一个分数，指示客户群体是否可能会响应广告活动。 若要执行所有这些操作，您需要创建一个预测查询。  
  
 就功能而言，SQL Server 中支持不同类型的预测查询，具体取决于查询的输入类型：  
  
|查询类型|查询选项|  
|----------------|-------------------|  
|单独预测查询|当您希望预测单个或多个新事例的结果时，可以使用单独查询。 可直接在查询中提供输入值，而查询作为单个会话执行。|  
|批预测|当您具有希望馈送到模型以用作预测基础的外部数据时，可以使用批预测。 若要对整个数据集进行预测，您可将外部源中的数据映射到模型中的列，然后指定希望输出的预测数据类型。<br /><br /> 对整个数据集的查询是在单个会话中执行的，这使得此选项要比发送多个重复的查询高效得多。|  
|时序预测|当您希望通过一些将来的步骤预测值，可以使用时序查询。 SQL Server 数据挖掘还在时序查询中提供以下功能：<br /><br /> 可以通过将新数据添加为查询的一部分来扩展现有模型，并基于组合序列进行预测。<br /><br /> 可以通过使用 REPLACE_MODEL_CASES 选项向新数据序列应用现有模型。<br /><br /> 可以执行交叉预测。|  
  
 以下部分介绍预测查询的一般语法、不同类型的预测查询以及如何使用预测查询的结果。  
  
 [基本的预测查询设计](#bkmk_PredQuery)  
  
-   [添加预测函数](#bkmk_PredFunc)  
  
-   [单独查询](#bkmk_SingletonQuery)  
  
-   [批预测查询](#bkmk_BatchQuery)  
  
 [使用查询结果](#bkmk_WorkResults)  
  
##  <a name="bkmk_PredQuery"></a> 基本的预测查询设计  
 创建预测时，通常会提供一些新数据，并要求模型基于新数据生成一个预测。  
  
-   在批预测查询中，可通过使用“预测联接” 将模型映射到外部数据源。  
  
-   在单独预测查询中，可键入一个或多个值以用作输入。 您可以使用单独预测查询来创建多个预测。 但是，如果您需要创建多个预测，那么使用批查询时的性能会更好。  
  
 单独预测查询和批预测查询都使用 PREDICTION JOIN 语法来定义新数据。 这两者的区别在于指定预测联接的输入端的方式。  
  
-   在批预测查询中，数据来自使用 OPENQUERY 语法指定的外部数据源。  
  
-   在单独预测查询中，数据是作为查询的一部分内联提供的。  
  
 对于时序模型，不总是需要输入数据；可以仅使用模型中现有的数据进行预测。 但是，如果您指定了新的输入数据，则必须确定是使用新数据更新和扩展模型，还是替换模型中已使用的原始数据序列。  有关这些选项的详细信息，请参阅 [Time Series Model Query Examples](time-series-model-query-examples.md)。  
  
###  <a name="bkmk_PredFunc"></a> 添加预测函数  
 除了预测值，您还可以自定义预测查询，以返回与预测有关的各种类型的信息。 例如，如果预测创建向客户推荐的产品的列表，则您还可能要返回每项预测的概率，以便可以对预测进行排名并且仅向用户展示最有价值的建议。  
  
 为此，您将向添加查询“预测函数”  。 每个模型或查询类型都支持特定的函数。 例如，聚类分析模型支持特殊预测函数，这些函数提供有关模型创建的分类的额外详细信息，而时序模型具有计算随时间的变化的函数。 还有可处理几乎所有模型类型的通用预测函数。 在不同类型的查询中受支持的预测函数的列表，请参阅主题 DMX 引用：[通用预测函数&#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)。  
  
###  <a name="bkmk_SingletonQuery"></a> 创建单独预测查询  
 如果要实时创建快速预测，则单独预测查询很有用。 一种常见情形可能是，您也许已通过使用网站上的窗体从客户获取了信息，希望提交这些数据作为单独预测查询的输入。 例如，当客户从列表中选择产品时，您可以使用所选内容作为预测最佳建议产品的查询的输入。  
  
 单独预测查询不需要包含输入的单独表。 而应将一行或多行值作为对模型的输入提供，并且将实时返回一个或多个预测。  
  
> [!WARNING]  
>  不管名称如何，单独预测查询并不只是生成单个预测 — 您可以生成为每个输入集的多个预测。 并且可以通过为每个输入事例创建一个 SELECT 语句并将它们与 UNION 操作符相结合，提供多个输入事例。  
  
 创建单独预测查询时，必须以 PREDICTION JOIN 的形式向模型提供新数据。 这意味着即使不映射到实际表，也必须确保新数据与挖掘模型中的现有列匹配。 如果新数据列与新数据完全匹配，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将自动映射列。 这称为“NATURAL PREDICTION JOIN” 。 但是，如果列不匹配，或者新数据在类型和量上与模型所包含的数据并不相同，则必须指定模型中的哪些列映射到新数据，或者指定缺少的值。  
  
###  <a name="bkmk_BatchQuery"></a> 批预测查询  
 如果您有想用来进行预测的外部数据，则批预测查询很有用。 例如，您可能已构建一个按客户的联机活动和购买历史记录对客户进行分类的模型。 您可以向最新获取的销售线索列表应用该模型，以创建销售投影或标识建议活动的目标。  
  
 当您执行预测联接时，必须将模型中的列映射到新数据源中的列。 因此，您选择作为输入的数据源所含数据必须与模型中的数据有些相似。 新信息不必完全匹配，也可以不完整。 例如，假定已使用与收入和年龄有关的信息对模型进行了定型，但您用于预测的客户列表具有年龄信息，却没有与收入有关的任何信息。 在此情况下，您仍可以将新数据映射到模型，并且为每个客户创建预测。 但是，如果收入已是模型的重要预测因子，则信息不完整将会影响预测的质量。  
  
 为获得最佳结果，应当在新数据与模型之间联接尽可能多的匹配列。 但是，即使没有匹配项，查询也会成功。 如果不联接任何列，则查询将返回边缘预测，这与不含 PREDICTION JOIN 子句的语句 `SELECT <predictable-column> FROM <model>` 是等效的。  
  
 您在成功映射所有相关列之后，即可运行查询，而 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将基于模型中的模式对新数据中的每一行进行预测。 您可以将结果保存回包含外部数据的数据源视图中的新表，也可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]复制粘贴这些数据。  
  
> [!WARNING]  
>  如果使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的设计器，则必须先将外部数据源定义为一个数据源视图。  
  
 如果使用 DMX 来创建预测联接，则可以通过使用 OPENQUERY、OPENROWSET 或 SHAPE 命令来指定外部数据源。 DMX 模板中的默认数据访问方法是 OPENQUERY。 有关这些方法的信息，请参阅 [<数据挖掘源数据>](/sql/dmx/source-data-query)。  
  
###  <a name="bkmk_TSQuery"></a> 时序挖掘模型中的预测  
 时序模型不同于其他模型类型；您既可以按原样使用模型来创建预测，也可以向模型中提供新数据来更新模型，并基于最近的趋势创建预测。 如果添加新数据，您可以指定应使用新数据的方式。  
  
-    “扩展模型事例”意味着向时序模型中的现有数据序列添加新数据。 自此以后，预测将基于新合并的序列。 如果只需向现有模型中添加几个数据点，则此选项是个不错的选择。  
  
     例如，假定您有一个现有的时序模型，它的上一年销售数据已定型。 收集了几个月的新销售数据后，您决定更新今年的销售预测。 您可以添加新数据并扩展模型以进行新预测，从而创建更新模型的预测联接。  
  
-    “替换模型事例”意味着您保留定型后的模型，但将基础事例替换为一组新的事例数据。 如果您希望保留模型中的趋势但将其应用到不同的一组数据，则此选项很有用。  
  
     例如，原始模型可能已定型于一组销售量非常高的数据之上；当您使用新序列（可能来自于销售量较低的存储区）替换基础数据时，可以保留趋势，但预测将从替换序列中的值开始。  
  
 无论您使用那种方法，预测的起点都总是原始序列的终点。  
  
 有关如何在时序模型上创建预测联接的详细信息，请参阅[时序模型查询示例](time-series-model-query-examples.md)或 [PredictTimeSeries (DMX)](/sql/dmx/predicttimeseries-dmx)。  
  
##  <a name="bkmk_WorkResults"></a> 处理预测查询的结果  
 您用于保存数据挖掘预测查询结果的选项取决于创建查询的方式。  
  
-   当您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中使用预测查询生成器生成查询时，可以将预测查询的结果保存到现有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源。 有关详细信息，请参阅 [查看和保存预测查询的结果](view-and-save-the-results-of-a-prediction-query.md)。  
  
-   当您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“查询”窗格使用 DMX 创建预测查询时，可以使用查询输出选项将结果保存到某一文件，或者作为文本保存到“查询结果”窗格或网格中。 有关详细信息，请参阅[查询和文本编辑器 (SQL Server Management Studio)](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)。  
  
-   当您使用 Integration Services 组件运行预测查询时，这些任务提供使用可用的 ADO.NET 连接管理器或 OLEDB 连接管理器将结果写入数据库的功能。 有关详细信息，请参阅 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)。  
  
 请务必了解，预测查询的结果与针对关系数据库的查询的结果不同，后者始终返回单行的相关值。 您添加到查询中的每个 DMX 预测函数都返回它自己的行集。 因此，当您针对一个事例进行预测时，结果可能是一个预测的值，以及包含其他详细信息的几个嵌套表列。  
  
 如果在一个查询中组合多个函数，则返回结果将组合为一个分层行集。 例如，假定您使用一个时序模型预测销售金额和销售数量的将来值，则使用以下 DMX 语句之类的查询：  
  
```  
SELECT  
  PredictTimeSeries([Forecasting].[Amount]) as [PredictedAmount]  
, PredictTimeSeries([Forecasting].[Quantity]) as [PredictedQty]  
FROM  
  [Forecasting]  
  
```  
  
 此查询的结果由两列构成，分别针对每个预测的序列，其中，每一行都包含具有预测值的嵌套表：  
  
 **PredictedAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|201101|172067.11|  
  
|$TIME|Amount|  
|-----------|------------|  
|201102|363390.68|  
  
 **PredictedQty**  
  
|$TIME|Quantity|  
|-----------|--------------|  
|201101|77|  
  
|$TIME|Quantity|  
|-----------|--------------|  
|201102|260|  
  
 如果提供程序无法处理分层的行集，则可以通过在预测查询中使用 FLATTEN 关键字来对结果进行平展处理。 有关详细信息，包括平展行集的示例，请参阅 [SELECT (DMX)](/sql/dmx/select-dmx)。  
  
## <a name="see-also"></a>请参阅  
 [内容查询（数据挖掘）](content-queries-data-mining.md)   
 [数据定义查询（数据挖掘）](data-definition-queries-data-mining.md)  
  
  
