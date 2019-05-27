---
title: 浏览数据 （SQL Server 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0bad2a2e65a65bbafa8218a3e0afbedd4b9f13b6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081310"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>浏览数据（SQL Server 数据挖掘外接程序）
  ![浏览数据向导](media/dmc-explore.gif "浏览数据向导")  
  
 **浏览数据**向导可帮助您了解类型和您的数据的表中的数据量。 向导图一次一列的分布和所选的列的值。 然后，您可尝试更改数据的分组方式，或将显示相应内容的图表复制到 Excel 工作簿中进行查看。  
  
 如果数据包含连续数值数据，可以在下面两种视图间切换：  
  
-   **线形图。** 此图表显示在 x 轴和 y 轴上的事例数的数据值。  
  
-   **条形图。** 条形图将值按照每个值的事例数进行分组。  
  
 当向导在数据中找到组时，它使用数据值的实际分布。 因此，条形图不显示典型的整数数值轴标记，如 10 或 100。 条形图中所显示的范围可能会像 43521-55603 这样（对于“收入”列）。  
  
 如果要按其他范围分组数据，则应当在分析数据前在 Excel 中执行此操作。 或者，可以使用重新标记数据[重新标记](relabel-sql-server-data-mining-add-ins.md)向导。  
  
## <a name="using-the-explore-data-wizard"></a>使用浏览数据向导  
  
1.  在中**数据挖掘**功能区中，单击**浏览数据**。  
  
2.  在中**选择源**对话框框中，选择表或包含你的数据单元格的范围。  
  
3.  在中**选择列**对话框框中，选择要分析，从显示的窗格中的示例数据的列。  
  
4.  在中**浏览数据**对话框框中，选择图表类型用于显示数据的分布情况。  
  
5.  此外，可以向数据中添加新列、更改数据分段方式，或将图表复制到 Excel。  
  
### <a name="requirements"></a>要求  
 若要使用**浏览数据**向导中，你的数据必须是在 Excel 数据表中。   
  
## <a name="see-also"></a>请参阅  
 [数据挖掘准备清单](checklist-of-preparation-for-data-mining.md)  
  
  
