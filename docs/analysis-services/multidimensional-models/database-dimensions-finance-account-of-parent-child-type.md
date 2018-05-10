---
title: 创建父-子类型维度的财务帐户 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 95006b55d6f77c0f8aff514c6d632182c717a7af
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="database-dimensions---finance-account-of-parent-child-type"></a>数据库维度的父-子类型的财务帐户
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，帐户类型的维度是指其属性表示用于财务报表用途的会计科目表的维度。  
  
 使用帐户维度，您可以有选择地管理一段时间内帐户间的聚合行为。 帐户维度还允许您使用标准机制来解决通常在处理财务数据的商业智能解决方案中遇到的大多非标准聚合问题。 如果不具有此标准机制，那么，解决这些非标准聚合问题就需要自定义汇总公式、计算成员或多维表达式 (MDX) 脚本。  
  
 若要将维度标识为帐户维度，请将维度的 **Type** 属性设置为 **Accounts**。  
  
## <a name="dimension-structure"></a>维度结构  
 帐户维度至少包含两种属性：  
  
-   键属性 - 标识帐户维度的维度表中各个帐户的属性。  
  
-   帐户属性 - 说明如何在帐户维度按层次结构排列帐户的父属性。  
  
     若要将特性标识为帐户特性，请将该特性的 **Type** 属性设置为 **Account** ，将 **Usage** 属性设置为 **Parent**。  
  
 帐户维度也可以包含以下属性：  
  
-   帐户类型属性 - 为维度中的每个帐户定义帐户类型的属性。 帐户类型属性的成员名称映射到为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库或项目定义的帐户类型，并指示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 针对那些帐户使用的聚合函数。 您也可以使用一元运算符或自定义汇总公式来决定帐户属性的聚合行为，但通过帐户类型可以轻松地将一致的行为应用于帐户图表，而无需对基础关系数据库进行更改。  
  
     若要标识帐户类型特性，请将该特性的 **Type** 属性设置为 **AccountType**。  
  
-   帐户名称属性 - 用于报表用途的属性。 您可以通过将特性的 **Type** 属性设置为 **AccountName**以标识帐户名称特性。  
  
-   帐号属性 - 用于报表用途的属性。 您可以通过将特性的 **Type** 属性设置为 **AccountNumber**来标识帐号特性。  
  
 有关属性类型的详细信息，请参阅 [配置属性类型](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md)。  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>通过商业智能向导添加帐户智能  
 定义帐户维度并将该维度添加到多维数据集后，可以使用商业智能向导添加帐户智能功能，例如，标识帐户类型，将帐户类型映射到维度。 有关详细信息，请参阅 [向维度中添加帐户智能](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [商业智能向导的 F1 帮助](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [维度类型](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
