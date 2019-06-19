---
title: KPI 浏览器 （Kpi 选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpibrowserpane.f1
ms.assetid: 2f61bde6-e6ec-4511-8645-c272374014ad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41000c78c4ff3a68e1d3acd107ce57c221a16e28
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079502"
---
# <a name="kpi-browser-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>KPI 浏览器（KPI 选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的“KPI”  选项卡上的“KPI 浏览器”  窗格查看和测试关键绩效指标 (KPI) 的结果。 在浏览之前，必须先将 KPI 部署到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。  
  
> [!NOTE]  
>  此窗格仅显示在浏览器视图中。  
  
## <a name="options"></a>选项  
 **子多维数据集网格**  
 用于定义子多维数据集和限制在“结果”  窗格中显示的 KPI 结果。 该网格包含以下列：  
  
 **Dimension**  
 选择应用此筛选器的维度。  
  
 **Hierarchy**  
 选择应用此筛选器的层次结构。  
  
 **“运算符”**  
 选择运算符，以定义“筛选表达式”  中的表达式如何应用于所选层次结构。 下表对可用的运算符进行了说明：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**Equal**|结果限制为在 **“筛选表达式”** 中定义的集合。|  
|**不等于**|结果限制为排除在 **“筛选表达式”** 中所定义集合之外的成员。|  
|**In**|结果限制为在 **“筛选表达式”** 中选择的命名集。|  
|**不在**|结果限制为排除在 **“筛选表达式”** 中所选命名集之外的成员。|  
|**包含**|结果限制为成员名称包含 **“筛选表达式”** 中的字符串的成员。|  
|**开始使用**|结果限制为成员名称以 **“筛选表达式”** 中的字符串开头的成员。|  
|**范围 （包括）**|结果限制为在 **“筛选表达式”** 中选择的范围。|  
|**范围 （不包括）**|结果限制为排除在 **“筛选表达式”** 中所选范围之外的成员。|  
|**MDX**|结果限制为在“筛选表达式”  中设置的多维表达式 (MDX) 表达式。|  
  
 **筛选表达式**  
 键入通过“运算符”  计算的表达式，该表达式可限制要浏览的 KPI 结果。  
  
> [!NOTE]  
>  此字段是动态数据输入元素，其外观将根据所选运算符的不同而相应改变，以反映该运算符所需的数据类型。  
  
 **结果网格**  
 基于“筛选器网格”  中定义的筛选器，显示 KPI 的计算结果值、目标、状态和走向。 该网格包含以下列：  
  
 **显示结构**  
 显示多维数据集包含的 KPI，按照每个 KPI 的“显示文件夹”  或“父 KPI”  值分层组织。  
  
 **ReplTest1**  
 显示 KPI 的值。  
  
 **目标**  
 显示 KPI 的目标值。  
  
 **“状态”**  
 显示 KPI 的状态图形。  
  
 **趋势**  
 显示 KPI 的走向图形。  
  
 **Weight**  
 显示 KPI 的加权系数。  
  
 **（说明）**  
 如果为 KPI 提供了说明，则显示信息图标。  
  
 将鼠标悬停在信息图标上方可以显示包含 KPI 说明的工具提示。  
  
> [!NOTE]  
>  如果在对 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例计算 KPI 时发生错误，此选项将显示与该错误关联的信息。  
  
## <a name="see-also"></a>请参阅  
 [Kpi&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
