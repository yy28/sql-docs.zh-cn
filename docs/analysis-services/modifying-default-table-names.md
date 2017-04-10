---
title: "修改默认表名 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: ddd97483-a76d-43c1-8b40-fc7cc57fb0c2
caps.latest.revision: 21
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 修改默认表名
可以在数据源视图中更改 **FriendlyName** 属性的值，以使它们更易于受人关注和使用。  
  
在下面的任务中，将从数据源视图中的每个表中删除“**Dim**”和“**Fact**”前缀来更改这些表的友好名称。 这会使将在下一课程中定义的多维数据集和维度对象变得更易于受人关注和使用。  
  
> [!NOTE]  
> 此外，还可以更改列的友好名称，定义计算列，以及联接数据源视图中的表或视图以使其变得更易于使用。  
  
### 修改表的默认名称  
  
1.  在“数据源视图设计器”的“表”窗格中右键单击 **FactInternetSales** 表，再单击“属性”。  
  
2.  如果在 Microsoft Visual Studio 窗口的右侧未显示“属性”窗口，则单击“属性”窗口的标题栏上的“自动隐藏”按钮，以便该窗口保持可见状态。  
  
    在“属性”窗口保持打开状态时，更容易更改数据源视图中各个表的属性。 如果不使用“自动隐藏”按钮使窗口保持打开状态，则在“关系图”窗格中单击其他对象时，该窗口将会关闭。  
  
3.  将 **FactInternetSales** 对象的 **FriendlyName** 属性更改为 ***InternetSales***。  
  
    如果在 **FriendlyName** 属性单元格外单击，则应用此更改。 在下一课中，将定义一个基于该事实数据表的度量值组。 由于您在本课中进行了更改，因此该事实数据表的名称将为 InternetSales，而不是 FactInternetSales。  
  
4.  在“表”窗格中单击 **DimProduct**。 在“属性”窗口中，将 **FriendlyName** 属性更改为“产品”。  
  
5.  使用同样的方法更改数据源视图中剩余的各个表的 **FriendlyName** 属性，删除“**Dim**”前缀。  
  
6.  完成更改后，单击“自动隐藏”按钮，重新隐藏“属性”窗口。  
  
7.  在“文件”菜单上，或者在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的工具栏上，单击“全部保存”，以保存截至目前已在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目中进行的更改。 您可以根据需要在此处停止教程学习，并在以后继续。  
  
## 下一课  
[第 2 课：定义和部署多维数据集](../analysis-services/lesson-2-defining-and-deploying-a-cube.md)  
  
## 另请参阅  
[多维模型中的数据源视图](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
[在数据源视图中更改属性 (Analysis Services)](../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  
  
