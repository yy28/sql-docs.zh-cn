---
title: 指定源信息（维度向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionmaintable.f1
ms.assetid: 0538b490-5185-49e1-a783-4ce3539a0de5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5015589854780f334dfa3b82b4f4ab544a4b7145
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940341"
---
# <a name="specify-source-information-dimension-wizard"></a>指定源信息（维度向导）
  可以使用 **“选择主维度表”** 页，为要创建的维度选择数据源视图、主维度表、键列和成员名列。  
  
 **打开维度向导**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的**解决方案资源管理器**中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目的“维度”文件夹，然后单击“新建维度”********。  
  
## <a name="options"></a>选项  
 **数据源视图**  
 选择数据源视图。  
  
 **主表**  
 从所选数据源视图中选择一个表，用作维度的主表。  
  
 **键列**  
 从维度的键属性的“主表”指定的表中选择键列。****  
  
> [!NOTE]  
>  您可以选择多列。 如果该表包含组合主键，则选择组合主键中包含的所有列。 键列的顺序很重要。  
  
 **名称列**  
 从提供维度成员名称的“主表”指定的表中选择列。**** 使用组合键时，必须指定名称列。 若要创建组合键的名称列，建议您在数据源视图中创建串联指定键列的命名计算。 使用单个键时，名称列是可选的。  
  
## <a name="see-also"></a>另请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [Analysis Services 多维数据 &#40;维度&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
