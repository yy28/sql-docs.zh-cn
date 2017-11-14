---
title: "类型元素 (DimensionAttribute) (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (DimensionAttribute)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 64fce1f5-39b7-4d0a-ae60-21203a03bd0d
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cd1ed987305726ea9e08eb507e2a1451d99e525b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-dimensionattribute-assl"></a>Type 元素 (DimensionAttribute) (ASSL)
  包含属性的类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
      ...  
   <Type>...</Type>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*正则*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*帐户*|该属性表示帐户的名称。|  
|*AccountNumber*|该属性表示帐户的编号。|  
|*AccountType*|该属性表示帐户的类型。|  
|*Address*|该属性表示地址。|  
|*AddressBuilding*|该属性表示地址中的建筑名。|  
|*AddressCity*|该属性表示地址中的市/县。|  
|*AddressCountry*|该属性表示地址中的国家（地区）。|  
|*AddressFax*|该属性表示传真号码。|  
|*AddressFloor*|该属性表示地址中的楼层号。|  
|*AddressHouse*|该属性表示地址中的楼牌号。|  
|*AddressPhone*|该属性表示电话号码。|  
|*AddressQuarter*|该属性表示地址中的区。|  
|*AddressRoom*|该属性表示地址中的房间号。|  
|*AddressStateOrProvince*|该属性表示地址中的省/市/自治区。|  
|*AddressStreet*|该属性表示地址中的街道名。|  
|*AddressZip*|该属性表示地址中的邮政编码。|  
|*BOMResource*|该属性表示物料清单 (BOM) 的资源。|  
|*标题*|该属性表示标题。|  
|*CaptionAbbreviation*|该属性表示缩写。|  
|*CaptionDescription*|该属性表示说明。|  
|*Channel*|该属性表示渠道。|  
|*城市*|该属性表示市。|  
|*公司*|该属性表示公司。|  
|*属于一个大洲*|该属性表示洲。|  
|*国家/地区*|该属性表示国家(地区)。|  
|*国家/地区*|该属性表示县。|  
|*CurrencyDestination*|该属性表示外币兑换的目标货币。|  
|*CurrencyISOcode*|该属性表示货币的 ISO 代码。|  
|*CurrencName*|该属性表示货币的名称。|  
|*CurrencySource*|该属性表示外币兑换中的源货币。|  
|*CustomerGroup*|该属性表示客户组。|  
|*CustomerHousehold*|该属性表示全体客户。|  
|*客户*|该属性表示客户。|  
|*日期*|该属性表示日期。|  
|*DateCanceled*|该属性表示取消日期。|  
|*DateDuration*|该属性表示持续时间。|  
|*DateEnded*|该属性表示结束日期。|  
|*DateModified*|该属性表示修改日期。|  
|*DateStart*|该属性表示开始日期。|  
|*DayOfHalfYears*|该属性表示每半年的第几天。|  
|*DayOfMonth*|该属性表示每月的第几天。|  
|*DayOfQuarter*|该属性表示每个季度的第几天。|  
|*DayOfTrimester*|该属性表示每四个月的第几天。|  
|*DayOfWeek*|该属性表示每周的第几天。|  
|*DayOfYear*|该属性表示每年的第几天。|  
|*天*|该属性表示日。|  
|*DaysOfTenDays*|该属性表示每十天的第几天。|  
|*FiscalDay*|该属性表示会计日历中的日。|  
|*FiscalDayOfHalfYears*|该属性表示会计日历中每半年的第几天。|  
|*FiscalDayOfMonth*|该属性表示会计日历中每月的第几天。|  
|*FiscalDayOfQuarter*|该属性表示会计日历中每个季度的第几天。|  
|*FiscalDayOfTrimester*|该属性表示会计日历中每四个月的第几天。|  
|*FiscalDayOfWeek*|该属性表示会计日历中每周的第几天。|  
|*FiscalDayOfYear*|该属性表示会计日历中每年的第几天。|  
|*FiscalHalfYears*|该属性表示会计日历中的半年。|  
|*FiscalHalfYearsOfYear*|该属性表示会计日历中每年的第几个半年。|  
|*财月*|该属性表示会计日历中的月。|  
|*FiscalMonthOfHalfYears*|该属性表示会计日历中每半年的第几个月。|  
|*FiscalMonthOfQuarter*|该属性表示会计日历中每个季度的第几个月。|  
|*FiscalMonthOfTrimester*|该属性表示会计日历中每四个月的第几个月。|  
|*FiscalMonthOfYear*|该属性表示会计日历中每年的第几个月。|  
|*FiscalQuarter*|该属性表示会计日历中的季度。|  
|*FiscalQuarterOfHalfYear*|该属性表示会计日历中每半年的第几个季度。|  
|*Fiscalquarterofyear 等*|该属性表示会计日历中每年的第几个季度。|  
|*FiscalTrimester*|该属性表示会计日历中的四个月。|  
|*FiscalTrimesterOfYear*|该属性表示会计日历中每年的第几个四个月。|  
|*FiscalWeek*|该属性表示会计日历中的周。|  
|*FiscalWeekOfHalfYears*|该属性表示会计日历中每半年的第几周。|  
|*FiscalWeekOfMonth*|该属性表示会计日历中每月的第几周。|  
|*FiscalWeekOfQuarter*|该属性表示会计日历中每个季度的第几周。|  
|*FiscalWeekOfTrimester*|该属性表示会计日历中每四个月的第几周。|  
|*FiscalWeekOfYear*|该属性表示会计日历中每年的第几周。|  
|*FiscalYear*|该属性表示会计日历中的年。|  
|*FormattingColor*|该属性表示设置格式时使用的颜色。|  
|*FormattingFont*|该属性表示设置格式时使用的字体。|  
|*FormattingFontEffects*|该属性表示设置格式时使用的字体效果。|  
|*FormattingFontSize*|该属性表示设置格式时使用的字号。|  
|*FormattingOrder*|该属性表示设置格式时使用的顺序。|  
|*FormattingSubtotal*|该属性表示小计。|  
|*GeoBoundaryBottom*|该属性表示地理边界的最底部的值。|  
|*GeoBoundaryFront*|该属性表示地理边界的最前面的值。|  
|*GeoBoundaryLeft*|该属性表示地理边界的最左侧的值。|  
|*GeoBoundaryPolygon*|该属性表示地理边界的多边形定义。|  
|*GeoBoundaryRear*|该属性表示地理边界的最后面的值。|  
|*GeoBoundaryRight*|该属性表示地理边界的最右侧的值。|  
|*GeoBoundaryTop*|该属性表示地理边界的最顶部的值。|  
|*GeoCentroidX*|该属性表示地理区域的 X 轴中点。|  
|*GeoCentroidY*|该属性表示地理区域的 Y 轴中点。|  
|*GeoCentroidZ*|该属性表示地理区域的 Z 轴中点。|  
|*HalfYears*|该属性表示半年。|  
|*HalfYearsOfYear*|该属性表示每年的第几个半年。|  
|*小时数*|该属性表示小时。|  
|*Id*|该属性表示标识符或键。|  
|*IsHoliday*|该属性指示某个日期是否为假日。|  
|*ISO8601DayOfWeek*|该属性表示 ISO 8601 日历中每周的第几天。|  
|*ISO8601DayOfYear*|该属性表示 ISO 8601 日历中每年的第几天。|  
|*ISO8601Days*|该属性表示 ISO 8601 日历中的日。|  
|*ISO8601Week*|该属性表示 ISO 8601 日历中的周。|  
|*ISO8601WeekOfYear*|该属性表示 ISO 8601 日历中每年的第几周。|  
|*ISO8601Year*|该属性表示 ISO 8601 日历中的年。|  
|*IsWeekDay*|该属性指示某个日期是否为正常的工作日（周一至周五）。|  
|*IsWorkingDay*|该属性指示某个日期是否为工作日（可包含周末）。|  
|*ManufacturingDay*|该属性表示生产日历中的日。|  
|*ManufacturingDayOfHalfYears*|该属性表示生产日历中每半年的第几天。|  
|*ManufacturingDayOfMonth*|该属性表示生产日历中每个月的第几天。|  
|*ManufacturingDayOfQuarter*|该属性表示生产日历中每个季度的第几天。|  
|*ManufacturingDayOfTrimester*|该属性表示生产日历中每四个月的第几天。|  
|*ManufacturingDayOfWeek*|该属性表示生产日历中每一周的第几天。|  
|*ManufacturingDayOfYear*|该属性表示生产日历中每一年的第几天。|  
|*ManufacturingHalfYears*|该属性表示生产日历中的半年。|  
|*ManufacturingHalfYearsOfYear*|该属性表示生产日历中每一年的第几个半年。|  
|*ManufacturingMonth*|该属性表示生产日历中的月。|  
|*ManufacturingMonthOfHalfYears*|该属性表示生产日历中每半年的第几个月。|  
|*ManufacturingMonthOfQuarter*|该属性表示生产日历中每个季度的第几个月。|  
|*ManufacturingMonthOfTrimester*|该属性表示生产日历中每四个月的第几个月。|  
|*ManufacturingMonthOfYear*|该属性表示生产日历中每一年的第几个月。|  
|*ManufacturingQuarter*|该属性表示生产日历中的季度。|  
|*ManufacturingQuarterOfHalfYear*|该属性表示生产日历中每半年的第几个季度。|  
|*ManufacturingQuarterOfYear*|该属性表示生产日历中每一年的第几个季度。|  
|*ManufacturingTrimester*|该属性表示生产日历中的每四个月。|  
|*ManufacturingTrimesterOfYear*|该属性表示生产日历中每一年的第几个四个月。|  
|*ManufacturingWeek*|该属性表示生产日历中的周。|  
|*ManufacturingWeekOfHalfYears*|该属性表示生产日历中每半年的第几周。|  
|*ManufacturingWeekOfMonth*|该属性表示生产日历中每月的第几周。|  
|*ManufacturingWeekOfQuarter*|该属性表示生产日历中每个季度的第几周。|  
|*ManufacturingWeekOfTrimester*|该属性表示生产日历中每四个月的第几周。|  
|*ManufacturingWeekOfYear*|该属性表示生产日历中每年的第几周。|  
|*ManufacturingYear*|该属性表示生产日历中的年。|  
|*Minutes*|该属性表示分钟。|  
|*MonthOfHalfYears*|该属性表示每半年的第几个月。|  
|*MonthOfQuarter*|该属性表示每个季度的第几个月。|  
|*MonthOfTrimester*|该属性表示每四个月的第几个月。|  
|*MonthOfYear*|该属性表示每一年的第几个月。|  
|*月*|该属性表示月。|  
|*OrganizationalUnit*|该属性表示部门。|  
|*OrgTitle*|该属性表示单位名称。|  
|*PercentOwnership*|该属性表示所有权百分比。|  
|*PercentVoteRight*|该属性表示投票权百分比。|  
|*人员*|该属性表示人员。|  
|*PersonContact*|该属性表示人员的联系信息。|  
|*PersonDemographic*|该属性表示人员的人口统计信息。|  
|*PersonFirstName*|该属性表示人员的名字。|  
|*PersonFullName*|该属性表示人员的全名。|  
|*PersonLastName*|该属性表示人员的姓氏。|  
|*PersonMiddleName*|该属性表示人员的中间名。|  
|*PhysicalColor*|该属性表示颜色。|  
|*PhysicalDensity*|该属性表示密度。|  
|*PhysicalDepth*|该属性表示深度。|  
|*PhysicalHeight*|该属性表示高度。|  
|*PhysicalSize*|该属性表示大小。|  
|*PhysicalVolume*|该属性表示体积。|  
|*PhysicalWeight*|该属性表示重量。|  
|*PhysicalWidth*|该属性表示宽度。|  
|*Point*|该属性表示点。|  
|*邮政编码*|该属性表示邮政编码。|  
|*Product*|该属性表示产品。|  
|*ProductBrand*|该属性表示产品品牌。|  
|*ProductCategory*|该属性表示产品类别。|  
|*ProductGroup*|该属性表示产品组。|  
|*ProductSKU*|该属性表示产品的单品 (SKU)。|  
|*ProjectCode*|该属性表示项目代码。|  
|*Projectcompletion*|该属性表示项目的完成状态。|  
|*ProjectEnddate*|该属性表示项目的结束日期。|  
|*项目名称*|该属性表示项目名称。|  
|*ProjectStartDate*|该属性表示项目的开始日期。|  
|*升级*|该属性表示促销。|  
|*QtyRangeHigh*|该属性表示数量范围的上限。|  
|*QtyRangeLow*|该属性表示数量范围的下限。|  
|*定量*|该属性表示定量属性。|  
|*QuarterOfHalfYear*|该属性表示每半年的第几个季度。|  
|*QuarterOfYear*|该属性表示每一年的第几个季度。|  
|*季度*|该属性表示季度。|  
|*速率*|该属性表示汇率。|  
|*RateType*|该属性表示汇率类型。|  
|地区|该属性表示客户定义的区域。|  
|*正则*|该属性表示常规属性。|  
|*RelationToParent*|该属性表示与父级的关系。|  
|*ReportingDay*|该属性表示报表日历中的日。|  
|*ReportingDayOfHalfYears*|该属性表示报表日历中每半年的第几天。|  
|*ReportingDayOfMonth*|该属性表示报表日历中每个月的第几天。|  
|*ReportingDayOfQuarter*|该属性表示报表日历中每个季度的第几天。|  
|*ReportingDayOfTrimester*|该属性表示报表日历中每四个月的第几天。|  
|*ReportingDayOfWeek*|该属性表示报表日历中每一周的第几天。|  
|*ReportingDayOfYear*|该属性表示报表日历中每一年的第几天。|  
|*ReportingHalfYears*|该属性表示报表日历中的半年。|  
|*ReportingHalfYearsOfYear*|该属性表示报表日历中每一年的第几个半年。|  
|*ReportingMonth*|该属性表示报表日历中的月。|  
|*ReportingMonthOfHalfYears*|该属性表示报表日历中每半年的第几个月。|  
|*ReportingMonthOfQuarter*|该属性表示报表日历中每个季度的第几个月。|  
|*ReportingMonthOfTrimester*|该属性表示报表日历中每四个月的第几个月。|  
|*ReportingMonthOfYear*|该属性表示报表日历中每一年的第几个月。|  
|*ReportingQuarter*|该属性表示报表日历中的季度。|  
|*ReportingQuarterOfHalfYear*|该属性表示报表日历中每半年的第几个季度。|  
|*ReportingQuarterOfYear*|该属性表示报表日历中每一年的第几个季度。|  
|*ReportingTrimester*|该属性表示报表日历中的每四个月。|  
|*ReportingTrimesterOfYear*|该属性表示报表日历中每一年的第几个四个月。|  
|*ReportingWeek*|该属性表示报表日历中的周。|  
|*ReportingWeekOfHalfYears*|该属性表示报表日历中每半年的第几周。|  
|*ReportingWeekOfMonth*|该属性表示报表日历中每个月的第几周。|  
|*ReportingWeekOfQuarter*|该属性表示报表日历中每个季度的第几周。|  
|*ReportingWeekOfTrimester*|该属性表示报表日历中每四个月的第几周。|  
|*ReportingWeekOfYear*|该属性表示报表日历中每年的第几周。|  
|*ReportingYear*|该属性表示报表日历中的年。|  
|*代表*|该属性表示代表。|  
|*方案*|该属性表示应用场景。|  
|*Seconds*|该属性表示秒。|  
|*序列*|该属性表示序列属性。|  
|*ShortCaption*|该属性表示短标题。|  
|*StateOrProvince*|该属性表示省/市/自治区。|  
|*TenDayOfHalfYears*|该属性表示每半年的第几个十天周期。|  
|*TenDayOfQuarter*|该属性表示每个季度的第几个十天周期。|  
|*TenDayOfTrimester*|该属性表示每四个月的第几个十天周期。|  
|*TenDayOfYear*|该属性表示每一年的第几个十天周期。|  
|*TenDays*|该属性表示为期十天的周期。|  
|*TenDaysOfMonth*|该属性表示每个月的第几个十天周期。|  
|*每四个月*|该属性表示四个月。|  
|*TrimesterOfYear*|该属性表示每一年的第几个四个月。|  
|*UndefinedTime*|该属性表示未定义的时间段。|  
|*实用工具*|该属性表示效用。|  
|*版本*|该属性表示版本。|  
|*WebHtml*|该属性表示 HTML 内容。|  
|*WebMailAlias*|该属性表示电子邮件别名。|  
|*WebUrl*|该属性表示 URL 地址。|  
|*WebXmlOrXsl*|该属性表示 XML 或 XSL 内容。|  
|*WeekOfHalfYears*|该属性表示每半年的第几周。|  
|*WeekOfMonth*|该属性表示每个月的第几周。|  
|*WeekOfQuarter*|该属性表示每个季度的第几周。|  
|*WeekOfTrimester*|该属性表示每四个月的第几周。|  
|*WeekOfYear*|该属性表示每年的第几周。|  
|*周*|该属性表示周。|  
|*年*|该属性表示年。|  
  
 对应于的允许值为枚举**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AttributeType>。  
  
 对应于的父元素**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另请参阅  
 [属性元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [维度元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

