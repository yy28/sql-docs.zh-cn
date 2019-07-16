---
title: 对挖掘结构的钻取 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6d2ea3d80496f84330802640ff99d951fd2416bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210041"
---
# <a name="drillthrough-on-mining-structures"></a>对挖掘结构的钻取功能
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “钻取”  意味着能够查询挖掘模型或挖掘结构并且获取在模型中未公开的详细数据。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供了两种不同的选项来钻取到事例数据中。 您可以钻取到用来挖掘模型的数据，也可以钻取到挖掘结构中的源数据。  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>钻取到模型事例与钻取到结构  
 钻取到“模型事例”  用于查找与模型中的规则、模式或群集有关的其他详细信息。  
  
 相反，“钻取到结构”  数据旨在提供对在模型中未提供的信息的访问。 例如，如果您具有适当的权限，则可能要确定哪些数据行已用于模型定型，哪些行已用于测试。  
  
 还可以查看在分析中未使用的数据属性，只要这些属性已包含在结构定义中。 例如，挖掘结构通常支持许多不同类型的模型，并且一些结构列可能已从模型中排除，因为数据类型不兼容或者数据未用于分析。 例如，您可能未在聚类分析模型中使用客户联系信息，即使数据已包含在结构中，但通过启用钻取，您能够不对数据源运行单独的查询就获取对此信息的访问权限。  
  
## <a name="enabling-drillthrough-to-structure-data"></a>对结构数据启用钻取  
 若要对挖掘结构使用钻取，必须满足以下条件：  
  
-   还必须对模型启用钻取。 默认情况下，这两种类型的钻取都被禁用。 若要在数据挖掘向导中启用钻取，请在向导的最后一页上选择该选项以便启用对模型事例的钻取。 您还可以通过更改 **AllowDrillthrough** 属性，在以后添加对模型的钻取功能。  
  
-   如果您使用 DMX 来创建挖掘结构，请使用 WITH DRILLTHROUGH 子句。 有关详细信息，请参阅 [CREATE MINING STRUCTURE (DMX)](../../dmx/create-mining-structure-dmx.md)。  
  
-   钻取就是检索在处理挖掘结构时缓存的定型事例的相关信息。 因此，如果在结构处理完毕后，通过将 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性更改为 **ClearAfterProcessing**，清除了缓存的数据，则钻取功能将无法正常工作。 若要对结构列启用钻取，则必须将 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性更改为 **KeepTrainingCases** ，然后重新处理结构。  
  
-   确认挖掘结构和挖掘模型都已将 [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) 属性设置为 **True**。 而且，您必须是对挖掘结构和挖掘模型都具有钻取权限的角色的成员。  
  
## <a name="security-issues-for-drillthrough"></a>钻取的安全问题  
 挖掘结构和挖掘模型的钻取权限是分开设置的。 即使不具有结构的钻取权限，模型的钻取权限也会允许您从模型进行钻取。 如果拥有结构的钻取权限，则可通过使用 [StructureColumn (DMX)](../../dmx/structurecolumn-dmx.md) 函数，将结构列包含到模型钻取查询中。  
  
 有关如何在 Analysis Services 中创建角色和分配权限的详细信息，请参阅[角色设计器（Analysis Services - 多维数据）](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192)。  
  
> [!NOTE]  
>  如果对挖掘结构和挖掘模型都启用了钻取，则只要用户是拥有挖掘模型的钻取权限的角色成员，就可以查看挖掘结构中的列，即使这些列并未包含在挖掘模型中，也是如此。 因此，为了保护敏感数据，应设置数据源视图来屏蔽个人信息，并且仅在需要时才允许对挖掘结构进行钻取访问。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何将钻取功能用于挖掘模型的详细信息，请参阅下列主题：  
  
|||  
|-|-|  
|从挖掘模型查看器对结构使用钻取|[从模型查看器使用钻取](../../analysis-services/data-mining/use-drillthrough-from-the-model-viewers.md)|  
|有关特定的模型类型，请参阅钻取查询的示例。|[数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)|  
|获取有关适用于特定挖掘结构和挖掘模型的权限的信息。|[授予数据挖掘结构和模型的权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>请参阅  
 [对挖掘模型的钻取功能](../../analysis-services/data-mining/drillthrough-on-mining-models.md)  
  
  
