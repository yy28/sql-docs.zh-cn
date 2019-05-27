---
title: 计算成员生成器对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.calculatedmemberbuilderdialog.f1
ms.assetid: 73b89a9f-f403-4ab8-99f7-e3ceb870c260
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8046d93f28c6d7c61899bb5f9aa3598f834c0ab3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088376"
---
# <a name="calculated-member-builder-dialog-box-analysis-services---multidimensional-data"></a>“计算成员生成器”对话框（Analysis Services - 多维数据）
  可以使用 **中的** “计算成员生成器” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框生成计算成员。  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**名称**|键入计算成员的名称。|  
|**父层次结构**|选择要在其中创建计算成员的层次结构。|  
|**父成员**|如果选择具有多个级别的父层次结构（`Measures` 维度除外），则将启用此选项。 单击省略号 (**...**) 按钮以选择父成员。 父成员确定计算成员在维度结构中的位置。|  
|**表达式**|键入要使用的 MDX 表达式。|  
|**检查**|单击 **“检查”** 可以测试 **“表达式”** 中定义的 MDX 表达式。|  
|**元数据**|显示可以包含在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] “表达式” **中所定义的 MDX 表达式中的当前**对象的元数据。<br /><br /> 通过右键单击所选项，然后选择“复制”，或者将所选项拖到“表达式”，可以复制所选项的 MDX 语法。|  
|**函数**|显示当前 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的可用 MDX 函数。 可以从 MDSCHEMA_FUNCTIONS 架构行集中检索所列项。<br /><br /> 通过右键单击所选项，然后选择“复制”，或者将所选项拖到“表达式”，可以复制所选项的 MDX 语法。|  
  
## <a name="see-also"></a>请参阅  
 [多维表达式 (MDX) 参考](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
