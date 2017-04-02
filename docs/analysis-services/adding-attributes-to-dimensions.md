---
title: "向维度添加属性 | Microsoft Docs"
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
ms.assetid: 80551dad-97ac-40d0-90af-b810780321ce
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 向维度添加属性
现在，您已经定义了维度，可以用表示维度中各数据元素的属性填充这些维度。 属性通常基于数据源视图中的字段。 在向维度中添加属性时，您可以在数据源视图中包括来自任何表的字段。  
  
在此任务中，将使用维度设计器向“客户”和“产品”维度中添加属性。 “客户”维度将包括基于“客户”和“地域”表中的字段的属性。  
  
## 向“客户”维度中添加属性  
  
#### 添加属性  
  
1.  打开“客户”维度的维度设计器。 为此，请在解决方案资源管理器的“维度”节点中双击“客户”维度。  
  
2.  在“属性”窗格中，请注意多维数据集向导已经创建的“客户关键字”和“地域关键字”属性。  
  
3.  在“维度结构”选项卡的工具栏上，确保用于在“数据源视图”窗格中查看表的“缩放”图标设置为 100%。  
  
4.  在“数据源视图”窗格中，将“Customer”表的以下各列拖到“属性”窗格中：  
  
    -   **BirthDate**  
  
    -   **MaritalStatus**  
  
    -   **性别**  
  
    -   **EmailAddress**  
  
    -   **YearlyIncome**  
  
    -   **TotalChildren**  
  
    -   **NumberChildrenAtHome**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **HouseOwnerFlag**  
  
    -   **NumberCarsOwned**  
  
    -   **Phone**  
  
    -   **DateFirstPurchase**  
  
    -   **CommuteDistance**  
  
5.  将“数据源视图”窗格内“Geography”表中的以下各列拖到“属性”窗格中：  
  
    -   **City**  
  
    -   **StateProvinceName**  
  
    -   **EnglishCountryRegionName**  
  
    -   **PostalCode**  
  
6.  在“文件”菜单上，单击“全部保存”。  
  
## 向“产品”维度中添加属性  
  
#### 添加属性  
  
1.  打开“产品”维度的维度设计器。 在解决方案资源管理器中，双击“产品”维度。  
  
2.  在“属性”窗格中，请注意多维数据集向导创建的“产品密钥”属性。  
  
3.  在“维度结构”选项卡的工具栏上，确保用于在“数据源视图”窗格中查看表的“缩放”图标设置为 100%。  
  
4.  将“数据源视图”窗格内“Product”表中的以下各列拖到“属性”窗格中：  
  
    -   **StandardCost**  
  
    -   **Color**  
  
    -   **SafetyStockLevel**  
  
    -   **ReorderPoint**  
  
    -   **ListPrice**  
  
    -   **Size**  
  
    -   **SizeRange**  
  
    -   **Weight**  
  
    -   **DaysToManufacture**  
  
    -   **ProductLine**  
  
    -   **DealerPrice**  
  
    -   **类**  
  
    -   **样式**  
  
    -   **ModelName**  
  
    -   **StartDate**  
  
    -   **EndDate**  
  
    -   **状态**  
  
5.  在“文件”菜单上，单击“全部保存”。  
  
## 课程中的下一个任务  
[检查多维数据集和维度属性](../analysis-services/reviewing-cube-and-dimension-properties.md)  
  
## 另请参阅  
[维度特性属性参考](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
  
