---
title: 查询和筛选器 （浏览器选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.filterpane.f1
ms.assetid: f5cf0bb1-3afb-4856-a2ef-614deb4e7e49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d788a4957d7c6b3ea02e407f8b09fa80b957a4b5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070537"
---
# <a name="query-and-filter-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>查询和筛选（“浏览器”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  多维数据集设计器中 **“浏览器”** 选项卡的这一区域包含查询和筛选区域，可帮助您从多维数据集中选择用于浏览或查询的数据。 您可以按需添加任意多个多维数据集对象，然后在数据区域中查看结果，或使用“在 Excel 中分析”功能将结果导出到报表，以便演示最终用户将如何查看数据。  
  
> [!WARNING]  
>  当您在此区域中处理数据时，默认情况下 **“浏览器”** 使用图形设计模式。 但是，您可以通过单击 **“设计模式”** 切换按钮使用 MDX 直接编辑该查询。 执行此操作时，用于设计维度筛选器的窗格会消失。 如果您想添加一个筛选器，可以切换回图形设计模式。  
  
 默认情况下，在执行查询时，当前用户的凭据（而非在 **“模拟信息”** 页中指定的凭据）用于连接到数据源。 但是，您也可以通过单击 **“工具栏”** 上的 **“更改用户”** 来更改查询或报表的用户上下文。  
  
## <a name="options"></a>选项  
 **Dimension**  
 选择对子多维数据集进行切片时所在的维度。  
  
 **Hierarchy**  
 选择对子多维数据集进行切片时所在的层次结构。  
  
 **“运算符”**  
 选择运算符，以定义“筛选表达式”中的表达式如何应用于所选层次结构。 下表对可用的运算符进行了说明：  
  
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
|**MDX**|结果限制为在“筛选表达式”中设置的多维表达式 (MDX) 表达式。|  
  
 **筛选表达式**  
 键入通过“运算符”计算的表达式，该表达式可限制要浏览的结果。  
  
> [!NOTE]  
>  此字段是动态数据输入元素，其外观将根据所选运算符的不同而相应改变，以反映该运算符所需的数据类型。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [浏览器&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [在 Excel 中分析&#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [元数据&#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
