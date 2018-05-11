---
title: 授予维度 (Analysis Services) 的权限 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cfad4f80d5ef06e9e16e48f6f4e6054b8d13c4db
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="grant-permissions-on-a-dimension-analysis-services"></a>授予维度的权限 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  维度安全用于设置维度对象（而非其数据）的权限。 通常，允许或拒绝访问处理操作是在设置维度权限时的主要目标。  
  
 但是，也许你的目标不是控制处理操作，而是控制维度的数据访问或其包含的属性和层次结构。 例如，具有不同地区销售部门的公司可能想要部门外人员不得接触销售绩效信息。 为了允许或拒绝不同组成人员访问某部分的维度数据，可以对属性和维度成员设置权限。 请注意，你无法拒绝对单个维度对象本身的访问，仅可拒绝对其数据的访问。 如果近期目标是允许或拒绝访问维度中的成员（包括对单个属性结构层次的访问权限），请参阅 [授予对维度数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 了解更多信息。  
  
 本主题的剩余部分包含对维度对象本身设置的权限，其中包括：  
  
-   读取或读/写权限（只可从读取或读/写选择；指定“无”不是选项）。 如上所述，如果目标是限制对维度数据的访问权限，请参阅 [授予对维度数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 了解详细信息。  
  
-   处理权限（当方案要求需要对单独的对象设置自定义权限的处理策略时，执行此项）  
  
-   读取定义权限（通常要支持工具中的交互式处理或对模型提供可见性时将会执行此项。 读取定义可以让你在没有维度数据的访问权限或无法修改其定义时看见维度的结构。）  
  
 在为维度定义角色时，可用维度根据对象是否为（位于数据库内部但在多维数据集外部的）独立数据库维度还是为多维数据集维度而变化。  
  
> [!NOTE]  
>  默认情况下，数据库维度的权限由多维数据集维度继承。 例如，如果启用“客户”数据库维度上的“读/写”权限，则“客户”多维数据集继承当前角色上下文的“读/写”权限。 如果要覆盖权限设置，则可以清除继承的权限。  
  
## <a name="set-permissions-on-a-database-dimension"></a>设置数据库维度权限  
 数据库维度是数据库内的独立对象，允许在相同模型内重复使用维度。 请考虑在模型中多次使用的“日期”数据库维度，如 Order Date、Ship Date 和 Due Date 多维数据集维度。 因为多维数据集维度和数据库维度为数据库中的同等对象，所以可以独立设置每个对象的处理权限。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，在对象资源管理器中展开相应数据库的“角色”，然后单击某个数据库角色（或创建一个新的数据库角色）。  
  
2.  在“维度”  窗格中，维度集应该设置为“所有数据库维度” 。  
  
     默认情况下，权限设置为“读取” 。  
  
     尽管“读/写”权限可用，但我们推荐不要使用此权限。 “读/写”用于维度写回情形下，而这已不推荐使用。 请参阅 [SQL Server 2016 中不推荐使用的 Analysis Services 功能](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md)。  
  
     此外，还可以对单独的维度对象设置“读取定义”  和“处理”  权限，前提是这些权限还未在数据库级别进行设置。 请参阅[授予处理权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) 和[授予对象元数据的读取定义权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md) 获取详细信息。  
  
## <a name="set-permissions-on-a-cube-dimension"></a>设置多维数据集维度权限  
 多维数据集维度是已添加到多维数据集的数据库维度。 因此，其在结构上依赖于关联的度量值组。 虽然可以在授权方面自动处理这些对象，但将多维数据集和多维数据集维度作为一个整体才有意义。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，在对象资源管理器中展开相应数据库的“角色”，然后单击某个数据库角色（或创建一个新的数据库角色）。  
  
2.  在**维度**窗格中，更改维度设置为\<多维数据集名称 >**多维数据集维度**。  
  
     默认情况下，权限继承自相应的数据库维度。 清除“继承”复选框，将权限从“读取”更改为“读/写”。 在使用“读/写”权限之前，请务必阅读上一节中的备注。  
  
> [!IMPORTANT]  
>  如果使用分析管理对象 (AMO) 配置数据库角色权限，那么，任何对多维数据集的 DimensionPermission 属性中多维数据集维度的引用都将切断对数据库的 DimensionPermission 属性的权限继承。 有关 AMO 的详细信息，请参阅[使用分析管理对象 (AMO) 进行开发](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)。  
  
## <a name="see-also"></a>另请参阅  
 [角色和权限 (Analysis Services)](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [授予多维数据集或模型权限 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [授予对数据挖掘结构和模型的权限&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [授予维度数据 & #40; 的自定义访问权限Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [授予单元数据 & #40; 的自定义访问权限Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  
