---
title: 添加或删除用户定义的层次结构 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00f65e2ed6b0633e1e76ea428ea671b392371ca0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="user-defined-hierarchies---add-or-delete-a-user-defined-hierarchy"></a>用户定义的层次结构-添加或删除用户定义的层次结构
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，可以从维度设计器中的“维度结构”选项卡上的维度中添加或删除用户定义的层次结构。  
  
 在添加用户定义的层次结构后，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中实例化此层次结构并且处理维度之前，用户无法使用此层次结构。 有关详细信息，请参阅[多维模型数据库](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)和[处理多维模型&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>向维度添加用户定义层次结构  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开相应的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，然后打开要使用的维度。  
  
     该维度会在维度设计器的 **“维度结构”** 选项卡上打开。  
  
2.  将要在用户定义的层次结构中使用的属性从“属性”窗格拖至“层次结构”窗格。  
  
3.  拖动其他属性以在用户定义层次结构中建立级别。  
  
     属性在层次结构中的列出顺序非常重要。 例如，在时间层次结构中，年在层次结构列表中的位置应高于日。  
  
4.  （可选）将用户定义层次结构中的级别拖至正确的位置，以便对这些级别进行重新排列。  
  
5.  （可选）修改用户定义层次结构或其级别的属性。  
  
     例如，您可能想为用户定义的层次结构指定名称，重命名它的一个或多个级别，以及为“全部”级别定义自定义名称。 有关详细信息，请参阅 [用户层次结构属性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)和 [级别属性 - 用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)。  
  
    > [!NOTE]  
    >  默认情况下，用户定义的层次结构仅仅是用户用于深化信息的路径。 但是，如果级别之间存在关系，则可以通过配置级别间的属性关系来提高查询性能。 有关详细信息，请参阅 [属性关系](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) 和 [定义属性关系](../../analysis-services/multidimensional-models/attribute-relationships-define.md)。  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>从维度中删除用户定义层次结构  
  
-   在“维度结构” 选项卡上的“层次结构”窗格中，单击要删除的用户定义的层次结构。 在工具栏上，单击 **“删除”**。  
  
     — 或者 —  
  
-   在“层次结构”窗格中右键单击要删除的用户定义的层次结构，然后单击“删除”。  
  
     — 或者 —  
  
-   将该用户定义的层次结构拖出设计图面。  
  
## <a name="see-also"></a>另请参阅  
 [用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [创建用户定义的层次结构](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
  
  
