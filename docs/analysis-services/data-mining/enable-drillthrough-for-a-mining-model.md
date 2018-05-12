---
title: 为挖掘模型启用钻取 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a928e8d49c815ad087b5baf19f9f85c7888c75dd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="enable-drillthrough-for-a-mining-model"></a>对挖掘模型启用钻取
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果为挖掘模型启用了钻取，则可以在浏览模型时检索用于创建模型的事例的详细信息。 若要查看这些信息，则您必须拥有必要的权限，且挖掘结构已经过处理。  
  
 **权限** 如果用户要钻取模型数据或结构数据，则该用户必须是具有挖掘模型或挖掘结构的 [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) 权限的角色成员。 挖掘结构和挖掘模型的钻取权限是分开设置的。  
  
-   即使不具有结构的钻取权限，模型的钻取权限也允许您从模型进行钻取。  
  
-   如果拥有结构的钻取权限，则可通过使用 [StructureColumn (DMX)](../../dmx/structurecolumn-dmx.md) 函数，将结构列包含到模型钻取查询中。 你还可以使用 SELECT… 从\<结构 >。用例语法。  
  
 **缓存定型事例** 钻取就是检索挖掘结构中的定型事例的相关信息。 这些信息是在处理结构时缓存的。 因此，如果通过将 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性更改为 **ClearAfterProcessing**，清除了缓存的数据，则钻取功能将无法正常工作。  
  
> [!NOTE]  
>  如果没有缓存定型事例，则必须将 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性更改为 **KeepTrainingCases** ，并重新处理模型，然后才能查看事例数据。  
  
 有关详细信息，请参阅[钻取查询（数据挖掘）](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>对挖掘模型启用钻取  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中数据挖掘设计器的“挖掘模型”选项卡上，右键单击要针对其启用钻取的挖掘模型名称，再选择“属性”。  
  
2.  在 **“属性”** 窗口中，单击 **AllowDrillthrough**，再选择 **True**。  
  
3.  在“挖掘模型”选项卡中，右键单击所需的模型，再选择“处理模型”。  
  
### <a name="to-enable-caching-for-a-mining-structure"></a>启用挖掘结构的缓存功能  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的数据挖掘设计器的“挖掘结构”选项卡上，右键单击挖掘结构的名称。  
  
2.  打开 **“属性”** 窗口。  
  
3.  在 **“属性”** 窗口中，找到 **CacheMode** 属性，然后从列表中选择 **KeepTrainingCases** 。  
  
4.  在 **“数据集”** 菜单上，选择 **“处理”**。  
  
## <a name="see-also"></a>另请参阅  
 [钻取查询 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
  
