---
title: "配置属性类型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time dimensions [Analysis Services]
- attributes [Analysis Services], types
- slowly changing dimensions
- account dimensions [Analysis Services]
- currency dimensions [Analysis Services]
- Type property
ms.assetid: c2c6a3da-555e-4362-a83f-88da28427520
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 60ccef2ddc36c4a8dda691526cb3209eb6737c6b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="attribute-properties---configure-attribute-types"></a>特性属性-配置属性类型
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，特性类型可用于按业务功能对特性进行分类。 特性类型的数目很多，其中的大部分都可由客户端应用程序用来显示或支持特性。 但是，某些特性类型对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]还有特定的含义。 例如，一些特性类型在时间维度的各种日历中用于标识代表时间段的特性。  
  
##  <a name="setting_attibute_types"></a> 设置特性类型  
 特性的 **Type** 属性值将确定该特性的特性类型。 在定义维度或特性时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的若干个向导可以对特性类型进行设置。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 向导在维度中添加功能时，也会设置特性类型。 例如，当商业智能向导添加帐户智能时，该向导将几个特性类型应用于维度中的特性，以标识包含维度中的名称、代码、编号和帐户结构的特性。 商业智能向导还可使用属性类型，例如用于货币换算。 有关详细信息，请参阅 [创建货币类型维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。  
  
 下表列出了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中可用的特性类型。 这些表将特性类型划分成以下类别：  
  
|术语|定义|  
|----------|----------------|  
|[常规特性类型](#general_attribute_types)|这些值可用于所有特性，使用它们只是为了针对客户端应用程序对特性进行归类。|  
|[帐户维度特性类型](#account_dimension_attribute_types)|这些值用于标识属于帐户维度的特性。 有关帐户维度的详细信息，请参阅 [创建父子类型维度的财务帐户](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)。|  
|[货币维度特性类型](#currency_dimension_attribute_types)|这些值用于标识属于货币维度的特性。 有关货币维度的详细信息，请参阅 [创建货币类型维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。|  
|[渐变维度特性](#slowly_changing_dimension_attribute_types)|这些值用于标识属于渐变维度的特性。|  
|[时间维度特性](#time_dimension_attribute_types)|这些值用于标识属于时间维度的特性。 有关时间维度的详细信息，请参阅 [创建日期类型维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)。|  
  
###  <a name="general_attribute_types"></a> General Attribute Types  
  
|特性类型值|Description|  
|--------------------------|-----------------|  
|**Address**|表示地址。|  
|**AddressBuilding**|表示地址中的建筑名。|  
|**AddressCity**|表示地址中的城市。|  
|**AddressCountry**|表示地址中的国家（地区）。|  
|**AddressFax**|表示传真电话号码。|  
|**AddressFloor**|表示地址中的楼层号。|  
|**AddressHouse**|表示地址中的楼牌号。|  
|**AddressPhone**|表示电话号码。|  
|**AddressQuarter**|表示地址中的区。|  
|**AddressRoom**|表示地址中的房间号。|  
|**AddressStateOrProvince**|表示地址中的省市自治区。|  
|**AddressStreet**|表示地址中的街道名。|  
|**AddressZip**|表示地址中的邮政编码。|  
|**BomResource**|表示物料清单 (BOM) 的资源。|  
|**Caption**|表示标题。|  
|**CaptionAbbreviation**|表示缩写。|  
|**CaptionDescription**|表示说明。|  
|**Channel**|表示渠道。|  
|**City**|表示市县。|  
|**Company**|表示公司。|  
|**洲**|表示洲。|  
|**Country**|表示国家（地区）。|  
|**County**|表示市县。|  
|**CustomerGroup**|表示客户组。|  
|**CustomerHousehold**|表示全体客户。|  
|**Customers**|表示客户。|  
|**DateCanceled**|表示取消日期。|  
|**DateDuration**|表示持续时间。|  
|**DateEnded**|表示结束日期。|  
|**DateModified**|表示修改日期。|  
|**DateStart**|表示开始日期。|  
|**DeletedFlag**|指示成员是否已删除或应当删除（在业务功能方面）。<br /><br /> 注意： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不用此特性类型来确定是否应删除成员。 此特性类型仅用于客户端应用程序显示。|  
|**FormattingColor**|表示设置格式时使用的颜色。|  
|**FormattingFont**|表示设置格式时使用的字体。|  
|**FormattingFontEffects**|表示设置格式时使用的字体效果。|  
|**FormattingFontSize**|表示设置格式时使用的字号。|  
|**FormattingOrder**|表示设置格式时使用的顺序。|  
|**FormattingSubtotal**|表示小计。|  
|**GeoBoundaryBottom**|表示地理边界的最底部的值。|  
|**GeoBoundaryFront**|表示地理边界前面的值。|  
|**GeoBoundaryLeft**|表示地理边界的最左侧的值。|  
|**GeoBoundaryPolygon**|表示地理边界的多边形定义。|  
|**GeoBoundaryRear**|表示地理边界的最后面的值。|  
|**GeoBoundaryRight**|表示地理边界的最右侧的值。|  
|**GeoBoundaryTop**|表示地理边界的最顶部的值。|  
|**GeoCentroidX**|表示地理区域的 X 轴中点。|  
|**GeoCentroidY**|表示地理区域的 Y 轴中点。|  
|**GeoCentroidZ**|表示地理区域的 Z 轴中点。|  
|**ID**|表示标识符 (ID) 或密钥。|  
|**图像**|表示未定义图形格式的图像。|  
|**ImageBmp**|表示位图图形格式的图像。|  
|**ImageGif**|表示图形交换格式 (GIF) 图形格式的图像。|  
|**ImageJpg**|表示联合图像专家组 (JPEG) 图形格式的图像。|  
|**ImagePng**|表示可移植网络图形 (PNG) 图形格式的图像。|  
|**ImageTiff**|表示标记图像文件格式 (TIFF) 图形格式的图像。|  
|**OrganizationalUnit**|表示部门。|  
|**OrgTitle**|表示单位名称。|  
|**PercentOwnership**|表示所有权百分比。|  
|**PercentVoteRight**|表示投票权百分比。|  
|**Person**|表示人员。|  
|**PersonContact**|表示人员的联系信息。|  
|**PersonDemographic**|表示人员的人口统计信息。|  
|**PersonFirstName**|表示人员的名字。|  
|**PersonFullName**|表示人员的全名。|  
|**PersonLastName**|表示人员的姓氏。|  
|**PersonMiddleName**|表示人员的中间名。|  
|**PhysicalColor**|表示颜色。|  
|**PhysicalDensity**|表示密度。|  
|**PhysicalDepth**|表示深度。|  
|**PhysicalHeight**|表示高度。|  
|**PhysicalSize**|表示大小。|  
|**PhysicalVolume**|表示体积。|  
|**PhysicalWeight**|表示重量。|  
|**PhysicalWidth**|表示宽度。|  
|**点**|表示点。|  
|**PostalCode**|表示邮政编码。|  
|**Product**|表示产品。|  
|**ProductBrand**|表示产品品牌。|  
|**ProductCategory**|表示产品类别。|  
|**ProductGroup**|表示产品组。|  
|**ProductSKU**|表示产品的单品 (SKU)。|  
|**项目**|表示项目。|  
|**ProjectCode**|表示项目代码。|  
|**ProjectCompletion**|表示项目的完成状态。|  
|**ProjectEndDate**|表示项目的结束日期。|  
|**ProjectName**|表示项目名称。|  
|**ProjectStartDate**|表示项目的开始日期。|  
|**Promotion**|表示促销。|  
|**QtyRangeHigh**|表示数量范围的上限。|  
|**QtyRangeLow**|表示数量范围的下限。|  
|**Quantitative**|表示定量特性。|  
|**Rate**|表示比率。|  
|**RateType**|表示比率类型。|  
|**地区**|表示客户定义地区。|  
|**Regular**|表示常规特性。|  
|**RelationToParent**|表示与父级的关系。|  
|**Representative**|表示代表。|  
|**应用场景**|表示方案。|  
|**序列**|表示序列特性。|  
|**ShortCaption**|表示短标题。|  
|**StateOrProvince**|表示省市自治区。|  
|**实用工具**|表示效用。|  
|**版本**|表示版本。|  
|**WebHtml**|表示 HTML 内容。|  
|**WebMailAlias**|表示电子邮件别名。|  
|**WebUrl**|表示 URL 地址。|  
|**WebXmlOrXsl**|表示 XML 或 XSL 内容。|  
  
###  <a name="account_dimension_attribute_types"></a> Account Dimension Attribute Types  
  
|特性类型值|Description|  
|--------------------------|-----------------|  
|**帐户**|表示父级帐户。 此特性类型通常应用于帐户维度的父级特性。|  
|**AccountName**|表示帐户的名称。 此特性类型通常应用于帐户维度的键特性。|  
|**AccountNumber**|表示帐户的编号。|  
|**AccountType**|表示帐户的类型。 此特性类型用于标识 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的帐户类型维度中的帐户成员的聚合函数。|  
  
###  <a name="currency_dimension_attribute_types"></a> 货币维度特性类型  
  
|特性类型值|Description|  
|--------------------------|-----------------|  
|**CurrencyDestination**|表示外币兑换的目标货币。 此特性类型通常应用于报表维度的键特性，在货币换算中使用。 有关货币换算的详细信息，请参阅[货币换算 (Analysis Services)](../../analysis-services/currency-conversions-analysis-services.md)。|  
|**CurrencyIsoCode**|表示货币的国际标准组织 (ISO) 代码。 有关货币换算的详细信息，请参阅[货币换算 (Analysis Services)](../../analysis-services/currency-conversions-analysis-services.md)。|  
|**CurrencyName**|表示货币的名称。 有关货币换算的详细信息，请参阅[货币换算 (Analysis Services)](../../analysis-services/currency-conversions-analysis-services.md)。|  
|**CurrencySource**|表示货币换算的源货币。 此特性类型通常应用于货币维度的键特性，在货币换算中使用。 有关货币换算的详细信息，请参阅[货币换算 (Analysis Services)](../../analysis-services/currency-conversions-analysis-services.md)。|  
  
###  <a name="slowly_changing_dimension_attribute_types"></a> 渐变维度特性类型  
  
|特性类型值|Description|  
|--------------------------|-----------------|  
|**ScdEndDate**|表示渐变维度中的成员的有效结束日期。|  
|**ScdOriginalID**|表示渐变维度中的成员的原始标识符。|  
|**ScdStartDate**|表示渐变维度中的成员的有效开始日期。|  
|**ScdStatus**|表示渐变维度中的成员的有效状态。|  
  
###  <a name="time_dimension_attribute_types"></a> 时间维度特性类型  
  
|特性类型值|Description|  
|--------------------------|-----------------|  
|**日期**|表示日期。 此特性类型通常应用于时间维度或服务器时间维度的键特性。|  
|**DayOfHalfYear**|表示每半年的第几天。|  
|**DayOfMonth**|表示每月的第几天。|  
|**DayOfQuarter**|表示每个季度的第几天。|  
|**DayOfTenDays**|表示每十天的第几天。|  
|**DayOfTrimester**|表示每四个月的第几天。|  
|**DayOfWeek**|表示每周的第几天。|  
|**DayOfYear**|表示每年的第几天。|  
|**Days**|表示天数。|  
|**FiscalDate**|表示会计日历中的日期。|  
|**FiscalDayOfHalfYear**|表示会计日历中半年的第几天。|  
|**FiscalDayOfMonth**|表示会计日历中每月的第几天。|  
|**FiscalDayOfQuarter**|表示会计日历中每个季度的第几天。|  
|**FiscalDayOfTrimester**|表示会计日历中每四个月的第几天。|  
|**FiscalDayOfWeek**|表示会计日历中每周的第几天。|  
|**FiscalDayOfYear**|表示会计日历中每年的第几天。|  
|**FiscalHalfYears**|表示会计日历中的半年数。|  
|**FiscalHalfYearOfYear**|表示会计日历中每年的第几个半年。|  
|**FiscalMonths**|表示会计日历中的月数。|  
|**FiscalMonthOfHalfYear**|表示会计日历中每半年的第几个月。|  
|**FiscalMonthOfQuarter**|表示会计日历中每个季度的第几个月。|  
|**FiscalMonthOfTrimester**|表示会计日历中每四个月的第几个月。|  
|**FiscalMonthOfYear**|表示会计日历中每一年的第几个月。|  
|**FiscalQuarters**|表示会计日历中的季度数。|  
|**FiscalQuarterOfHalfYear**|表示会计日历中每半年的第几个季度。|  
|**FiscalQuarterOfYear**|表示会计日历中每年的第几个季度。|  
|**FiscalTrimesters**|表示会计日历中的四个月。|  
|**FiscalTrimesterOfYear**|表示会计日历中每一年的第几个四个月。|  
|**FiscalWeeks**|表示会计日历中的周数。|  
|**FiscalWeekOfHalfYear**|表示会计日历中每半年的第几周。|  
|**FiscalWeekOfMonth**|表示会计日历中每月的第几周。|  
|**FiscalWeekOfQuarter**|表示会计日历中每个季度的第几周。|  
|**FiscalWeekOfTrimester**|表示会计日历中每四个月的第几周。|  
|**FiscalWeekOfYear**|表示会计日历中每年的第几周。|  
|**FiscalYears**|表示会计日历中的年数。|  
|**HalfYears**|表示半年。|  
|**HalfYearOfYear**|表示每年的第几个半年。|  
|**Hours**|表示小时。|  
|**IsHoliday**|指示某天是否为假日。|  
|**ISO8601Date**|表示 ISO 8601 日历中的日期。|  
|**ISO8601DayOfWeek**|表示 ISO 8601 日历中每周的第几天。|  
|**ISO8601DayOfYear**|表示 ISO 8601 日历中每年的第几天。|  
|**ISO8601Weeks**|表示 ISO 8601 日历中的周。|  
|**ISO8601WeekOfYear**|表示 ISO 8601 日历中每年的第几周。|  
|**ISO8601Years**|表示 ISO 8601 日历中的年。|  
|**IsPeakDay**|指示日期是否是高峰日。|  
|**IsWeekDay**|指示日期是否为周工作日。|  
|**IsWorkingDay**|指示日期是否为工作日。|  
|**ManufacturingDate**|表示生产日历中的日期。|  
|**ManufacturingDayOfHalfYear**|表示生产日历中每半年的第几天。|  
|**ManufacturingDayOfMonth**|表示生产日历中每个月的第几天。|  
|**ManufacturingDayOfQuarter**|表示生产日历中每个季度的第几天。|  
|**ManufacturingDayOfTrimester**|表示生产日历中每四个月的第几天。|  
|**ManufacturingDayOfWeek**|表示生产日历中每一周的第几天。|  
|**ManufacturingDayOfYear**|表示生产日历中每一年的第几天。|  
|**ManufacturingHalfYears**|表示生产日历中的半年数。|  
|**ManufacturingHalfYearOfYear**|表示生产日历中每一年的第几个半年。|  
|**ManufacturingMonths**|表示生产日历中的月数。|  
|**ManufacturingMonthOfHalfYear**|表示生产日历中每半年的第几个月。|  
|**ManufacturingMonthOfQuarter**|表示生产日历中每个季度的第几个月。|  
|**ManufacturingMonthOfTrimester**|表示生产日历中每四个月的第几个月。|  
|**ManufacturingMonthOfYear**|表示生产日历中每一年的第几个月。|  
|**ManufacturingQuarters**|表示生产日历中的季度数。|  
|**ManufacturingQuarterOfHalfYear**|表示生产日历中每半年的第几个季度。|  
|**ManufacturingQuarterOfYear**|表示生产日历中每一年的第几个季度。|  
|**ManufacturingWeeks**|表示生产日历中的周数。|  
|**ManufacturingWeekOfHalfYear**|表示生产日历中每半年的第几周。|  
|**ManufacturingWeekOfMonth**|表示生产日历中每月的第几周。|  
|**ManufacturingWeekOfQuarter**|表示生产日历中每个季度的第几周。|  
|**ManufacturingWeekOfTrimester**|表示生产日历中每四个月的第几周。|  
|**ManufacturingWeekOfYear**|表示生产日历中每年的第几周。|  
|**ManufacturingYears**|表示生产日历中的年数。|  
|**Minutes**|表示分钟数。|  
|**Months**|表示月数。|  
|**MonthOfHalfYear**|表示每半年的第几个月。|  
|**MonthOfQuarter**|表示每个季度的第几个月。|  
|**MonthOfTrimester**|表示每四个月的第几个月。|  
|**MonthOfYear**|表示每一年的第几个月。|  
|**Quarters**|表示季度数。|  
|**QuarterOfHalfYear**|表示每半年的第几个季度。|  
|**QuarterOfYear**|表示每一年的第几个季度。|  
|**ReportingDate**|表示报表日历中的日期。|  
|**ReportingDayOfHalfYear**|表示报表日历中每半年的第几天。|  
|**ReportingDayOfMonth**|表示报表日历中每个月的第几天。|  
|**ReportingDayOfQuarter**|表示报表日历中每个季度的第几天。|  
|**ReportingDayOfTrimester**|表示报表日历中每四个月的第几天。|  
|**ReportingDayOfWeek**|表示报表日历中每一周的第几天。|  
|**ReportingDayOfYear**|表示报表日历中每一年的第几天。|  
|**ReportingHalfYears**|表示报表日历中的半年数。|  
|**ReportingHalfYearOfYear**|表示报表日历中每一年的第几个半年。|  
|**ReportingMonths**|表示报表日历中的月数。|  
|**ReportingMonthOfHalfYear**|表示报表日历中每半年的第几个月。|  
|**ReportingMonthOfQuarter**|表示报表日历中每个季度的第几个月。|  
|**ReportingMonthOfTrimester**|表示报表日历中每四个月的第几个月。|  
|**ReportingMonthOfYear**|表示报表日历中每一年的第几个月。|  
|**ReportingQuarters**|表示报表日历中的季度数。|  
|**ReportingQuarterOfHalfYear**|表示报表日历中每半年的第几个季度。|  
|**ReportingQuarterOfYear**|表示报表日历中每一年的第几个季度。|  
|**ReportingTrimesters**|表示报表日历中的每四个月。|  
|**ReportingTrimesterOfYear**|表示报表日历中每一年的第几个四个月。|  
|**ReportingWeeks**|表示报表日历中的周数。|  
|**ReportingWeekOfHalfYear**|表示报表日历中每半年的第几周。|  
|**ReportingWeekOfMonth**|表示报表日历中每个月的第几周。|  
|**ReportingWeekOfQuarter**|表示报表日历中每个季度的第几周。|  
|**ReportingWeekOfTrimester**|表示报表日历中每四个月的第几周。|  
|**ReportingWeekOfYear**|表示报表日历中每年的第几周。|  
|**ReportingYears**|表示报表日历中的年。|  
|**Seconds**|表示秒数。|  
|**TenDayOfHalfYear**|表示每半年的第几个十天周期。|  
|**TenDayOfMonth**|表示每个月的第几个十天周期。|  
|**TenDayOfQuarter**|表示每个季度的第几个十天周期。|  
|**TenDayOfTrimester**|表示每四个月的第几个十天周期。|  
|**TenDayOfYear**|表示每一年的第几个十天周期。|  
|**TenDays**|表示为期十天的周期数。|  
|**Trimesters**|表示每四个月数。|  
|**TrimesterOfYear**|表示每一年的第几个四个月。|  
|**UndefinedTime**|表示未定义的时间段。|  
|**WeekOfYear**|表示每年的第几周。|  
|**Weeks**|表示周数。|  
|**WinterSummerSeason**|指示日期是否属于冬季/夏季。|  
|**Years**|表示年数。|  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [维度特性属性参考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
