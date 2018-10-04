---
title: KPI 窗体编辑器 （Kpi 选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpidefinitionpane.f1
ms.assetid: 45c6453a-bbe2-4ca5-836e-c7ef11cfcb65
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49df3dcaf89d98d42da0a89ea7de0b8114093913
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166377"
---
# <a name="kpi-form-editor-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>KPI 窗体编辑器（KPI 选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的“KPI”选项卡上的“KPI 窗体编辑器”窗格，创建或修改所选的关键绩效指标 (KPI)。  
  
> [!NOTE]  
>  此窗格仅显示在窗体视图中。  
  
## <a name="options"></a>选项  
 **名称**  
 键入 KPI 的名称。  
  
 **关联的度量值组**  
 选择与 KPI 关联的度量值组。 客户端应用程序可以使用此信息来确定当用户浏览此 KPI 时哪些维度可用。  
  
 **值表达式**  
 展开此项可以查看或编辑 KPI 值的多维表达式 (MDX) 表达式。  
  
 键入返回 KPI 的值的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 **目标表达式**  
 展开此项可以查看或编辑 KPI 的目标值的 MDX 表达式。  
  
 键入当 KPI 运行时返回 KPI 的目标值的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 **“状态”**  
 展开此项可以查看“状态图形”和“状态表达式”选项。  
  
 **状态图形**  
 选择客户端应用程序用来以图形形式显示状态值的图形。  
  
> [!NOTE]  
>  客户端应用程序可以支持所选的图形，或将其替换为适当的替代项。  
  
 **状态表达式**  
 键入当 KPI 运行时返回 KPI 的状态值的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 建议此表达式返回 –1 和 1 之间的十进制数字。 数字越小表示情况越差，数字越大表示情况越好。  
  
> [!NOTE]  
>  可能有小于 –1 或大于 1 的值，但是它们可能无法被第三方客户端应用程序正确解释。  
  
 **趋势**  
 展开此项可以查看“走向图”和“走向表达式”选项。  
  
 **走向图**  
 选择客户端应用程序用来以图形形式显示走向值的图形。  
  
> [!NOTE]  
>  客户端应用程序可以支持所选的图形，或将其替换为适当的替代项。  
  
 **走向表达式**  
 键入返回 KPI 的走向值的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 走向表达式可以基于在给定的业务上下文中有意义的任何基于时间的条件。 建议此表达式返回 –1 和 1 之间的十进制数字。 较小的数字表示随着时间的推移情况会越来越差，较大的数字表示随着时间的推移情况会越来越好。  
  
> [!NOTE]  
>  可能有小于 –1 或大于 1 的值，但是它们可能无法被第三方客户端应用程序正确解释。  
  
 **附加属性**  
 展开此项可以查看“显示文件夹”、“父级 KPI”、“当前时间成员”、“权重”和“说明”选项。  
  
 **显示文件夹**  
 键入客户端应用程序在显示时所使用的 KPI 分类。  
  
 在显示文件夹中使用反斜杠 (\\) 分隔文件夹名称，并使用分号 (;) 分隔多个显示文件夹。 例如，键入 `Category\Goal\Scientific;Category\Goal\Metric`。  
  
 **父级 KPI**  
 选择一个现有 KPI，将在其下对 KPI 进行分类以供客户端应用程序使用。  
  
> [!NOTE]  
>  如果将此选项设置为现有 KPI，则忽略“显示文件夹”。  
  
 **当前时间成员**  
 键入返回用于标识 KPI 临时上下文的成员的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
> [!IMPORTANT]  
>  MDX 表达式必须在与“关联的度量值组”中指定的度量值组关联的时间维度内返回唯一的成员名称。  
  
 **Weight**  
 展开此项可以查看或编辑 KPI 加权系数的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 **Description**  
 键入 KPI 的说明（可选）。  
  
## <a name="see-also"></a>请参阅  
 [Kpi&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
