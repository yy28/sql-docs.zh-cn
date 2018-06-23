---
title: 浏览数据 （SQL Server 数据挖掘外接程序） |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c648fba4cf47f117eb5dd04b76b5d7f0cb4f17c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025350"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>浏览数据（SQL Server 数据挖掘外接程序）
  ![浏览数据向导](media/dmc-explore.gif "浏览数据向导")  
  
 **浏览数据**向导可帮助你了解的类型和您数据的表中的数据量。 向导图一次一个列的分发和所选的列的值。 然后，您可尝试更改数据的分组方式，或将显示相应内容的图表复制到 Excel 工作簿中进行查看。  
  
 如果数据包含连续数值数据，可以在下面两种视图间切换：  
  
-   **折线图。** 此图表显示在 x 轴和 y 轴上的事例数上的数据值。  
  
-   **条形图。** 条形图将值按照每个值的事例数进行分组。  
  
 当向导在数据中找到组时，它使用数据值的实际分布。 因此，条形图不显示典型的整数数值轴标记，如 10 或 100。 条形图中所显示的范围可能会像 43521-55603 这样（对于“收入”列）。  
  
 如果要按其他范围分组数据，则应当在分析数据前在 Excel 中执行此操作。 或者，你可以通过使用数据重新标记发生[重新标记](relabel-sql-server-data-mining-add-ins.md)向导。  
  
## <a name="using-the-explore-data-wizard"></a>使用浏览数据向导  
  
1.  在**数据挖掘**功能区上，单击**浏览数据**。  
  
2.  在**选择源**对话框框中，选择的表或包含你的数据的单元格范围。  
  
3.  在**Select 列**对话框框中，选择要分析，从示例数据窗格中显示的列。  
  
4.  在**浏览数据**对话框框中，选择显示的分布的数据的图表类型。  
  
5.  此外，可以向数据中添加新列、更改数据分段方式，或将图表复制到 Excel。  
  
### <a name="requirements"></a>要求  
 若要使用**浏览数据**向导中，你的数据必须是在 Excel 数据表。   
  
## <a name="see-also"></a>请参阅  
 [数据挖掘准备清单](checklist-of-preparation-for-data-mining.md)  
  
  