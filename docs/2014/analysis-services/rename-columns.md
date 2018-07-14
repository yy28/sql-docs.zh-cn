---
title: 第 3 课： 重命名列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d4f9d156889bd3a761cff2a18a908df42e8aade
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246091"
---
# <a name="lesson-3-rename-columns"></a>第 3 课：重命名列
  在本课中，您将重命名您导入的每个表中的很多列。 通过重命名，您可以更易于识别列，且更易于在模型设计器中以及通过用户在客户端应用程序中选择字段来进行导航列。 若要了解详细信息，请参阅[重命名表或列（SSAS 表格）](tabular-models/rename-a-table-or-column-ssas-tabular.md)。  
  
> [!IMPORTANT]  
>  重命名列对于完成本教程不是必需的；但剩下的课程（尤其是包含使用 DAX 公式来创建关系、创建计算列和度量值的课程）将引用在本课中介绍的列友好名称。 如果您选择不重命名列，则必须编辑第 5、6 和 7 课中的 DAX 公式，以便使用本课中提供的原始源列名称。  
  
 学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>必要條件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 执行本课中的任务之前，须已完成上一课： [第 2 课：添加数据](lesson-2-add-data.md)。  
  
## <a name="rename-columns"></a>对列重命名  
  
#### <a name="to-rename-columns"></a>对列进行重命名  
  
1.  在模型设计器中，单击“Customer”表（选项卡）。  
  
     单击某个选项卡时，该表将在模型设计器窗口中变为活动状态。  
  
2.  双击**CustomerKey**列的名称，然后键入`Customer  Id`，然后按 ENTER。  
  
    > [!TIP]  
    >  还可以在列的“属性”窗口的“列名”属性中或在“关系图视图”中对列重命名。  
  
3.  重命名 **Customer** 表中的其余列以及其余表中的列，用友好名称替换源名称：  
  
     **Customer 表**  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |CustomerAlternateKey|Customer Alternate Id|  
    |FirstName|First Name|  
    |MiddleName|Middle Name|  
    |LastName|Last Name|  
    |NameStyle|Name Style|  
    |BirthDate|Birth Date|  
    |MaritalStatus|婚姻状况|  
    |EmailAddress|Email Address|  
    |YearlyIncome|Yearly Income|  
    |TotalChildren|Total Children|  
    |NumberChildrenAtHome|Number of Children At Home|  
    |EnglishEducation|教育|  
    |EnglishOccupation|职业|  
    |HouseOwnerFlag|Owns House|  
    |NumberCarsOwned|Number of Cars Owned|  
    |AddressLine1|Address Line 1|  
    |AddressLine2|Address Line 2|  
    |Phone|Phone Number|  
    |DateFirstPurchase|Date of First Purchase|  
    |CommuteDistance|上下班路程|  
  
     **Date**  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |FullDateAlternateKey|date|  
    |DayNumberOfWeek|Day Number of Week|  
    |EnglishDayNameOfWeek|Day Name|  
    |DayNumberOfMonth|Day of Month|  
    |DayNumberOfYear|Day of Year|  
    |WeekNumberOfYear|Week Number of Year|  
    |EnglishMonthName|Month Name|  
    |MonthNumberOfYear|Month|  
    |CalendarQuarter|Calendar Quarter|  
    |CalendarYear|Calendar Year|  
    |CalendarSemester|Calendar Semester|  
    |FiscalQuarter|Fiscal Quarter|  
    |FiscalYear|Fiscal Year|  
    |FiscalSemester|Fiscal Semester|  
  
     **地域**  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |StateProvinceCode|State Province Code|  
    |StateProvinceName|State Province Name|  
    |CountryRegionCode|Country Region Code|  
    |EnglishCountryRegionName|Country Region Name|  
    |PostalCode|Postal Code|  
    |SalesTerritoryKey|Sales Territory Id|  
  
     **Product**  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |ProductAlternateKey|Product Alternate Id|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |WeightUnitMeasureCode|Weight Unit Code|  
    |SizeUnitMeasureCode|Size Unit Code|  
    |EnglishProductName|产品名称|  
    |StandardCost|标准成本|  
    |FinishedGoodsFlag|Is Finished Product|  
    |SafetyStockLevel|Safety Stock Level|  
    |ReorderPoint|Reorder Point|  
    |ListPrice|标价|  
    |SizeRange|Size Range|  
    |DaysToManufacture|Days to Manufacture|  
    |ProductLine|Product Line|  
    |经销价格|经销价格|  
    |ModelName|Model Name|  
    |LargePhoto|Large Photo|  
    |EnglishDescription|Description|  
    |StartDate|Product Start Date|  
    |EndDate|Product End Date|  
    |“登录属性”|Product Status|  
  
     **产品类别**  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |ProductCategoryKey|Product Category Id|  
    |ProductCategoryAlternateKey|Product Category Alternate Id|  
    |EnglishProductCategoryName|Product Category Name|  
  
     **产品子类别**  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |ProductSubcategoryAlternateKey|Product Subcategory Alternate Id|  
    |EnglishProductSubcategoryName|Product Subcategory Name|  
    |ProductCategoryKey|Product Category Id|  
  
     **Internet Sales**  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |CustomerKey|Customer Id|  
    |PromotionKey|Promotion Id|  
    |CurrencyKey|Currency Id|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesOrderNumber|Sales Order Number|  
    |SalesOrderLineNumber|Sales Order Line Number|  
    |RevisionNumber|修订号|  
    |OrderQuantity|Order Quantity|  
    |UnitPrice|Unit Price|  
    |ExtendedAmount|Extended Amount|  
    |UnitPriceDiscountPct|Unit Price Discount Pct|  
    |DiscountAmount|Discount Amount|  
    |ProductStandardCost|Product Standard Cost|  
    |TotalProductCost|Total Product Cost|  
    |SalesAmount|Sales Amount|  
    |TaxAmt|税额|  
    |CarrierTrackingNumber|Carrier Tracking Number|  
    |CustomerPONumber|Customer PO Number|  
    |OrderDate|Order Date|  
    |DueDate|Due Date|  
    |ShipDate|Ship Date|  
  
## <a name="next-step"></a>下一步  
 若要继续学习本教程，请转到下一课： [第 4 课：标记为日期表](lesson-3-mark-as-date-table.md)。  
  
  
