---
title: "维度中的设置的属性的自定义成员公式 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Business Intelligence enhancements [Analysis Services], custom member formulas
- member formulas [Analysis Services]
- dimensions [Analysis Services], Business Intelligence enhancements
- custom member formulas [Analysis Services]
- CustomRollupColumn property
ms.assetid: c4467b08-ce59-4de7-a2d9-c22e246bdd52
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f6cd6ca41dab2aa9d213281de94882c03f50db2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="bi-wizard---custom-member-formulas-for-attributes-in-a-dimension"></a>BI 向导-维度中的属性的自定义成员公式
  通过在多维数据集或维度中添加自定义成员公式增强功能，可以使用多维表达式 (MDX) 表达式的结果替换与维度成员关联的默认聚合。 （此增强功能将设置维度中的指定特性的 **CustomRollupColumn** 属性。）  
  
> [!NOTE]  
>  自定义成员公式只对基于现有数据源的维度可用。 对于不使用数据源所创建的维度，则必须运行架构生成向导，以便在添加自定义成员公式之前创建数据源视图。  
  
 若要添加自定义成员公式，请使用商业智能向导，并在 **“选择增强功能”** 页上选择 **“创建自定义成员公式”** 选项。 然后，此向导将指引您完成相应的步骤，以选择要应用自定义成员公式的维度，并启用自定义成员公式。  
  
## <a name="selecting-a-dimension"></a>选择维度  
 在向导的第一个 **“创建自定义成员公式”** 页中，指定希望应用自定义成员公式的维度。 添加到此所选维度中的自定义成员公式增强功能将使维度发生更改。 所有包含选定维度的多维数据集都将继承这些更改。  
  
## <a name="enabling-a-custom-member-formula"></a>启用自定义成员公式  
 在第二个 **“创建自定义成员公式”** 页中，将包含自定义成员公式的源列与维度中的一个或多个属性关联。 在 **“属性”** 列中，选中要与自定义成员公式列关联的属性旁边的复选框。 选择每个属性之后，向导将显示 **“选择列”** 对话框。 在此对话框中，单击包含公式的维度表中的列。 如果在关闭“选择列”对话框之后希望更改选择，请单击希望更改的“源列”单元，再单击省略号 (**...**) 以再次打开“选择列”对话框。  
  
## <a name="see-also"></a>另请参阅  
 [使用商业智能向导增强维度](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
  
  
