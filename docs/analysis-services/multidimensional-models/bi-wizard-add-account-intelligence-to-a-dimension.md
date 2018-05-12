---
title: 向维度中添加帐户智能 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5021d10832028f46d1d0b1a8f33dc01a75df5985
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="bi-wizard---add-account-intelligence-to-a-dimension"></a>BI 向导-向维度中添加帐户智能
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在多维数据集或维度中添加帐户智能增强功能，以向具有某一帐户属性的成员分配标准帐户分类，如收入和支出。 这种增强功能还可以标识帐户类型（如“资产”和“负债”）并为每种帐户类型分配适当的聚合。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以随着时间的推移使用分类来聚合帐户。  
  
> [!NOTE]  
>  帐户智能仅可用于基于现有数据源的维度。 对于不使用数据源创建的维度，必须先运行架构生成向导创建数据源视图，然后再添加帐户智能。  
  
 您可以将帐户智能应用于指定帐户信息（如帐户名、帐号以及帐户类型）的维度。 若要添加帐户智能，请使用商业智能向导，并在 **“选择增强功能”** 页中选择 **“定义帐户智能”** 选项。 然后，该向导引导您完成下列步骤：选择要应用帐户智能的维度、标识选定帐户维度中的帐户属性以及将维度表中的帐户类型映射到由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]识别的帐户类型。  
  
## <a name="selecting-a-dimension"></a>选择维度  
 在向导的第一个 **“定义帐户智能”** 页中，指定要应用帐户智能的维度。 已添加到该选定维度中的帐户智能增强功能将会使维度发生更改。 所有包含选定维度的多维数据集都将继承这些更改。  
  
## <a name="specifying-account-attributes"></a>指定帐户属性  
 在向导的 **“配置维度属性”** 页中，指定选定帐户维度中的帐户属性。 首先，在 **“包括”** 列中，选中要映射到维度中维度属性的每个帐户属性类型旁边的复选框。 然后，在“维度属性”列中，展开下拉列表，并选择维度中对应于选定属性类型的属性。 从列表中选择特性会设置帐户特性的 **Type** 属性。  
  
## <a name="mapping-account-types"></a>映射帐户类型  
 第二个 **“定义帐户智能”** 页将维度表中的帐户类型值映射到由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]识别的帐户类型。 仅当维度中包含 **“帐户类型”** 维度属性时，才出现该页。 若要包含 **“帐户类型”** 维度，请在向导的 **“定义帐户智能设置”** 页中，选中 **“帐户类型”**旁边的复选框，然后选择相应的属性。  
  
 在第二个 **“定义帐户智能”** 页中，具有两个列：  
  
-   **“源表帐户类型”** 列，列出向导从维度表中获取的帐户类型。  
  
-   **“服务器帐户类型”** 列，标识由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 识别的对应帐户类型。 下表列出了由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 识别的帐户类型以及每个类型的默认聚合。 如果维度表与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用相同的帐户类型名称，则会自动进行选择。  
  
    |服务器帐户类型|聚合|Description|  
    |-------------------------|-----------------|-----------------|  
    |**统计**|**InclusionThresholdSetting**|某事物的计算比率，或者未在某段时间内聚合的某事物的计数。 该帐户类型不会使用换算规则在各种货币之间进行换算。|  
    |**负债**|**LastNonEmpty**|在特定时间所拖欠的现金或事物的价值。 该帐户类型不会随时间而积累，因此，不会随时间而自然聚合。 例如，“年”数量是指具有数据的上一个月的值。 该帐户类型使用“期末”汇率在各种货币之间进行换算。|  
    |**资产**|**LastNonEmpty**|在特定时间所拥有的现金或事物的价值。 该帐户类型随时间而积累，因此，不会随时间而自然聚合。 例如，“年”数量是指具有数据的上一个月的值。 该帐户类型使用“期末”汇率在各种货币之间进行换算。|  
    |**平衡**|**LastNonEmpty**|在特定时间某事物的计数。 该帐户类型随时间而积累，但不会随时间而自然聚合。 例如，“年”数量是指具有数据的上一个月的值。|  
    |**流**|**Sum**|某事物的增量计数。 该帐户类型随时间而聚合为 **Sum** ，但不会使用货币换算规则进行换算。|  
    |**费用**|**Sum**|所花费的现金或事物的价值。 该帐户类型随时间而聚合为 **Sum** ，并可使用平均汇率在各种货币之间进行换算。|  
    |**收入**|**Sum**|所收到的现金或事物的价值。 该帐户类型随时间而聚合为 **Sum** ，并可使用平均汇率在各种货币之间进行换算。|  
  
    > [!NOTE]  
    >  如果需要，您可以将维度中的多个帐户类型映射到某个特定的服务器帐户类型。  
  
 若要更改数据库映射到每个帐户类型的默认聚合，可以使用数据库设计器。  
  
1.  在解决方案资源管理器中，右键单击 Analysis Services 项目，再单击“编辑数据库”。  
  
2.  在 **“帐户类型映射”** 框的 **“名称”**中，选择帐户类型。  
  
3.  在 **“别名”** 文本框中，键入此帐户类型的别名。  
  
4.  在 **“聚合函数”** 下拉列表框中，更改此帐户类型的默认聚合函数。  
  
  
