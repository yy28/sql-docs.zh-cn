---
title: 添加或删除用户定义层次结构 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], adding
- removing hierarchies
- adding hierarchies
- deleting hierarchies
- hierarchies [Analysis Services], removing
ms.assetid: 953818b4-9543-4c01-bb20-1d45ec6dfb91
caps.latest.revision: 50
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3cb9b55bcff41dddd2a4c648854e92222d1e8e2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157118"
---
# <a name="add-or-delete-a-user-defined-hierarchy"></a>添加或删除用户定义层次结构
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，可以从维度设计器中的“维度结构”选项卡上的维度中添加或删除用户定义的层次结构。  
  
 在添加用户定义的层次结构后，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中实例化此层次结构并且处理维度之前，用户无法使用此层次结构。 有关详细信息，请参阅[多维模型数据库&#40;SSAS&#41; ](multidimensional-model-databases-ssas.md)并[多维模型对象处理](processing-a-multidimensional-model-analysis-services.md)。  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>向维度添加用户定义层次结构  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开相应的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，然后打开要使用的维度。  
  
     该维度会在维度设计器的 **“维度结构”** 选项卡上打开。  
  
2.  将要在用户定义的层次结构中使用的属性从“属性”窗格拖至“层次结构”窗格。  
  
3.  拖动其他属性以在用户定义层次结构中建立级别。  
  
     属性在层次结构中的列出顺序非常重要。 例如，在时间层次结构中，年在层次结构列表中的位置应高于日。  
  
4.  （可选）将用户定义层次结构中的级别拖至正确的位置，以便对这些级别进行重新排列。  
  
5.  （可选）修改用户定义层次结构或其级别的属性。  
  
     例如，您可能想为用户定义的层次结构指定名称，重命名它的一个或多个级别，以及为“全部”级别定义自定义名称。 有关详细信息，请参阅[用户层次结构属性](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)，并[级别的属性&#91;Paved 通过&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)。  
  
    > [!NOTE]  
    >  默认情况下，用户定义的层次结构仅仅是用户用于深化信息的路径。 但是，如果级别之间存在关系，则可以通过配置级别间的属性关系来提高查询性能。 有关详细信息，请参阅 [属性关系](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) 和 [定义属性关系](attribute-relationships-define.md)。  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>从维度中删除用户定义层次结构  
  
-   在“维度结构” 选项卡上的“层次结构”窗格中，单击要删除的用户定义的层次结构。 在工具栏上，单击 **“删除”**。  
  
     — 或者 —  
  
-   在“层次结构”窗格中右键单击要删除的用户定义的层次结构，然后单击“删除”。  
  
     — 或者 —  
  
-   将该用户定义的层次结构拖出设计图面。  
  
## <a name="see-also"></a>请参阅  
 [用户层次结构](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [创建用户定义的层次结构](user-defined-hierarchies-create.md)  
  
  
