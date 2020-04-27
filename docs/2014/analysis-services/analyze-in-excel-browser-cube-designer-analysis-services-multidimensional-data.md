---
title: 在 Excel 中分析（"浏览器" 选项卡，多维数据集设计器）（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.datapane.f1
- sql12.asvs.ssms.analyzeinexcel.f1
ms.assetid: 890ed457-137e-44ac-9b2c-83344a1b8fc9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b2833fb2ecbbac269442ce149cd5673abedcf83c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062369"
---
# <a name="analyze-in-excel-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>在 Excel 中分析（“浏览器”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  **“在 Excel 中分析”** 为多维数据集开发人员提供了一种快速检查项目将如何呈现给最终用户的方式。 使用 **“在 Excel 中分析”** 功能可以打开 Microsoft Excel、创建到模型工作区数据库的数据源连接，以及自动将数据透视表添加到工作表。 此功能将取代 Office Web Control，后者在以前版本的“浏览器”选项卡中提供了一个嵌入的数据透视表。  
  
 **查看多维数据集数据：**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]的解决方案资源管理器中，双击某一多维数据集以在多维数据集设计器中打开它。  
  
2.  单击 **“浏览器”** 选项卡。  
  
3.  单击 **“重新连接”** 以便对连接进行验证。  
  
4.  单击菜单栏中的 Excel 图标。  
  
5.  在系统提示您启用数据连接时，单击 **“启用”**。 Excel 将使用当前数据连接打开，并且向电子表格中添加一个数据透视表，以便您可以开始浏览数据。  
  
 您可以通过将度量值从事实表拖到“值”区域，并且将维度属性拖到“行”和“列”区域，以交互方式生成数据透视表。 如果您具有层次结构，则将它们添加到“行”和“列”区域。 您可以汇总或深化层次结构，以便在不同级别浏览事实数据。  
  
 在有效用户或角色的上下文以及透视中查看对象和数据。 在使用 Excel 时，默认情况下，在执行查询时，当前用户的凭据（而非在 **“模拟信息”** 页中指定的凭据）用于连接到数据源。  
  
> [!NOTE]  
>  为了使用“在 Excel 中分析”功能，Excel 必须与 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]安装在同一台计算机上。 如果 Excel 安装在不同的计算机上，您可以在另一计算机上使用 Excel 并连接到作为数据源的多维数据集。 然后可以将数据透视表手动添加到工作表。 模型对象（表、列、度量值和 KPI）作为数据透视表字段列表中的字段包含。  
  
 有关 **“在 Excel 中分析”** 功能的详细信息，请参阅以下资源：  
  
 [在 Excel 中分析（SSAS 表格）](tabular-models/analyze-in-excel-ssas-tabular.md)  
  
 [在 Excel 中分析表格模型（SSAS 表格）](tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)  
  
 [浏览多维数据集中的数据和元数据](multidimensional-models/browse-data-and-metadata-in-cube.md)  
  
## <a name="see-also"></a>另请参阅  
 [浏览器 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏 &#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [元数据 &#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [查询和筛选 &#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
