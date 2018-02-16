---
title: "钻取查询 （数据挖掘） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AllowDrillThrough property
- drillthrough [Analysis Services]
- drillthrough [DMX]
ms.assetid: 246c784b-1b0c-4f0b-96f7-3af265e67051
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2ac1295dcbea5ff575cb0d1d5ab918bad03c6fd0
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="drillthrough-queries-data-mining"></a>钻取查询（数据挖掘）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
“钻取查询”  让您通过将查询发送到挖掘模型，检索基础事例或结构数据中的详细信息。 如果您希望查看用来为模型定型的事例以及用来测试模型的事例，或者如果您希望查看事例数据的详细信息，则钻取会非常有用。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据挖掘提供了两种不同的钻取选项：  
  
-   钻取到 **模型事例**  
  
     如果您希望从模型中的某个特定模式（如群集或决策树的分支）钻取，则使用钻取到“模型事例”，并查看有关单个事例的详细信息。  
  
-   钻取到 **结构事例**  
  
     如果结构中包含模型中可能不可用的信息，则使用钻取到结构事例。 例如，即使结构中包括客户联系信息，也不在聚类分析模型中使用该数据。 但是，在创建聚类分析模型之后，您可能希望检索那些分组到特定分类中的客户的联系信息。  
  
 本节提供有关如何创建这些查询的示例。  
  
 [在数据挖掘设计器中使用钻取](#bkmk_Designer)  
  
 [使用 DMX 来创建钻取查询](#bkmk_DMX)  
  
 [使用钻取功能时的注意事项](#bkmk_Considerations)  
  
-   [安全性问题](#bkmk_Security)  
  
-   [限制](#bkmk_Limits)  
  
##  <a name="bkmk_Designer"></a> 在数据挖掘设计器中使用钻取  
 如果挖掘模型已经配置为允许进行钻取，而且如果您具有适当的权限，那么，当您浏览模型时，可以在相应的查看器中单击某个节点，并检索有关该特定节点中各个事例的详细信息。  
  
 [从挖掘模型钻取到事例数据](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)。  
  
 如果处理挖掘结构时缓存了定型事例，并且您具有必要的权限，则您可以从模型事例和挖掘结构返回信息（包括挖掘模型中没有的列）。  
  
##  <a name="bkmk_DMX"></a> 使用 DMX 来创建钻取查询  
 如果您对模型或结构具有权限，则可以通过创建 DMX 查询来钻取到事例数据。 有关在 DMX 中创建钻取查询的语法的示例，请参阅以下主题：  
  
 [创建使用 DMX 的钻取查询](../../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)  
  
##  <a name="bkmk_Considerations"></a> 使用钻取功能时的注意事项  
  
-   如果使用数据挖掘向导，则用以对模型事例启用钻取的选项位于向导的最后一页。 默认情况下，钻取功能处于禁用状态。 有关详细信息，请参阅[完成向导（数据挖掘向导）](http://msdn.microsoft.com/library/6aef1548-35eb-42fd-ae87-63650a79eda1)。  
  
-   您可以向现有的挖掘模型中添加钻取功能，但是，如果这样做，必须重新处理该模型，才能钻取到所需的数据。  
  
-   钻取就是检索在处理挖掘结构时缓存的定型事例的相关信息。 因此，如果在结构处理完毕后，通过将 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性更改为 **ClearAfterProcessing**，清除了缓存的数据，则钻取功能将无法正常工作。 若要对结构列启用钻取，则必须将 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性更改为 **KeepTrainingCases** ，然后重新处理结构。  
  
-   如果挖掘结构不允许进行钻取，但是挖掘模型允许进行钻取，则只能查看模型事例中的信息，而不能查看挖掘结构中的信息。  
  
###  <a name="bkmk_Security"></a> 钻取的安全问题  
 如果您希望从模型钻取到结构事例，则必须确认挖掘结构和挖掘模型的 [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) 属性均设置为 **True**。 而且，您必须是对挖掘结构和挖掘模型都具有钻取权限的角色的成员。 有关如何创建角色的信息，请参阅[角色设计器（Analysis Services - 多维数据）](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192)。 请参阅。  
  
 挖掘结构和挖掘模型的钻取权限是分开设置的。 即使不具有结构的钻取权限，模型的钻取权限也会允许您从模型进行钻取。 如果拥有结构的钻取权限，则可通过使用 [StructureColumn (DMX)](../../dmx/structurecolumn-dmx.md) 函数，将结构列包含到模型钻取查询中。  
  
> [!NOTE]  
>  如果对挖掘结构和挖掘模型都启用了钻取，则只要用户是拥有挖掘模型的钻取权限的角色成员，就可以查看挖掘结构中的列，即使这些列并未包含在挖掘模型中，也是如此。 因此，为了保护敏感数据，应设置数据源视图来屏蔽个人信息，并且仅在需要时才允许对挖掘结构进行钻取访问。  
  
###  <a name="bkmk_Limits"></a> 钻取限制  
  
-   下面的限制适用于针对模型的钻取操作，具体情况取决于用来创建模型的算法：  
  
|算法名称|问题|  
|--------------------|-----------|  
|Microsoft Naïve Bayes 算法|不提供支持。 这些算法不为内容中的特定节点分配事例。|  
|Microsoft 神经网络算法|不提供支持。 这些算法不为内容中的特定节点分配事例。|  
|Microsoft 逻辑回归算法|不提供支持。 这些算法不为内容中的特定节点分配事例。|  
|Microsoft 线性回归算法|支持。 但是，由于该模型创建一个节点 ( **All**)，因此钻取时会返回该模型的所有定型事例。 如果定型集非常大，则加载结果可能会需要很长时间。|  
|Microsoft 时序算法|支持。 但是，不能通过使用数据挖掘设计器的 **“挖掘模型查看器”** 来钻取到结构或事例数据， 而必须创建一个 DMX 查询。<br /><br /> 同样，不能钻取到特定节点，也不能编写一个 DMX 查询来检索时序模型内特定节点中的事例。 可以通过使用其他条件（如日期或属性值）来从模型或结构中检索事例数据。<br /><br /> 还可使用 [Lag (DMX)](../../dmx/lag-dmx.md) 函数，从模型中的事例返回日期。<br /><br /> 如果希望查看由 Microsoft 时序算法创建的 ARTXP 和 ARIMA 节点的详细信息，则可使用 [Microsoft 一般内容树查看器（数据挖掘）](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)。|  
  
##  <a name="bkmk_Tasks"></a> 相关任务  
 通过以下链接在特定方案中使用钻取。  
  
|任务|链接|  
|----------|----------|  
|描述在数据挖掘设计器中使用钻取的过程|[从挖掘模型钻取到事例数据](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)|  
|改变现有的挖掘模型以允许钻取|[为挖掘模型启用钻取](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)|  
|使用 DMX WITH DRILLTHROUGH 子句对挖掘模型启用钻取。|[创建挖掘结构 &#40; DMX &#41;](../../dmx/create-mining-structure-dmx.md)|  
|有关分配适用于对挖掘结构和挖掘模型进行钻取的权限的信息|[授予对数据挖掘结构和模型 &#40; 的权限Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘模型查看器](../../analysis-services/data-mining/data-mining-model-viewers.md)   
 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
