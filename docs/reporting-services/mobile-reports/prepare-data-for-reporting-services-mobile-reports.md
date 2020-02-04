---
title: 为 Reporting Services 移动报表准备数据 | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 8adce9ad-6a08-4d20-b1cf-d3c45544d8de
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9ded496c3509420d54325dc054e018048ede0732
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "62499917"
---
# <a name="prepare-data-for-reporting-services-mobile-reports"></a>Prepare data for Reporting Services mobile reports
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] 支持大量复杂的数据操作，包括筛选、聚合和时间切分。 本文介绍了准备数据时需要牢记的几个要点。 预先聚合数据可以优化移动报表的创建和使用，并且某些移动报表设计也需要它。   
  
## <a name="date-and-time-formats"></a>日期和时间格式 
当处理日期和时间间隔以便用于移动报表，尤其是处理 TimeNavigator 时，正确设置日期/时间列的格式至关重要，以便 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 可以根据此设置进行识别。 以下是有效的日期/时间格式的示例：  
  
    05/01/2009    
    2009-05-01    
    05/01/2009 14:57:32.8    
    2009-05-01 14:57:32.8    
    2009-05-01T14:57:32.8375298-04:00    
    5/01/2008 14:57:32.80 -07:00    
    1 May 2008 2:57:32.8 PM    
    Fri, 15 May 2009 20:10:57 GMT    
  
在大多数情况下，基于日期和时间的数据集都可以采用一个或多个日期/时间间隔进行描述，例如，每小时、每天、每月、每季度和每年。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 可以组合多个具有不同粒度的表并将其显示在单个移动报表中。 但要记住原始数据集中的相关间隔时间，因为这将有助于确定向最终移动报表中的用户显示何种日期/时间筛选器选项。  

[!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 多维和表格模型中的数据字段可能在共享数据集中丢失其日期格式。 有关保留其格式的解决方案，请参阅 [保留移动报表中 Analysis Services 数据的日期格式](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) 。
  
## <a name="preparing-filter-data"></a>准备筛选数据 ##  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 可以根据日期/时间字段和键字段筛选数据。 虽然键字段可以是数字，但在大多数情况下，它们要么是一个 ID，要么是一个字符串值。 若要准备与导航元素（如选择列表）配合使用的筛选器字段，筛选键在数据表中应为单列。 这样你便可以根据筛选器列中的值对表中的各行进行分组。 使多个列包含不同的筛选键或筛选条件，可以使具有多个筛选导航器的移动报表分层次地一起进行使用或单独使用。  
  
| 行业  | 国家/地区   | 区域    |  
| ------------- | ------------- | ------------- |  
| 银行     | 阿富汗   | 亚洲      |  
| 商业和专业服务 | 阿富汗 | 亚洲 |  
| 食物饮料和烟草行业 | 阿富汗 | 亚洲 |  
| 媒体 | 阿富汗 | 亚洲 |  
| 医药业 | 阿富汗 | 亚洲 |  
| 食物和必需品零售业 | 阿尔巴尼亚 | 欧洲 |  
  
  
基于键的筛选器还可以具有层次结构，以便在树结构中与“选项列表”配合使用。 若要准备用于此类型方案的数据，可创建描述分层结构的查找表。 使用包含键列和父级键列的表结构，指示节点在整个层次结构中的所属位置。  
  
在此表中，ParentKey 项首先在 ItemKey 列中列出，然后在其子项旁的 ParentItemKey 列中列出。   
  
|ItemKey    | ParentItemKey |  
| ------------- | ------------- |  
| 金融    |   |  
| 工业   |   |  
| 消费者日常用品 |    |  
| 非必需消费品 |  |     
| 健康保健   |   |  
| 信息技术 |  |  
| 银行 | 金融 |  
| 房地产 | 金融 |  
| 多元化金融 |  金融 |   
| 保险 |   金融 |  
| 商业和专业服务 |  工业 |  
| 资本货物 |   工业 |  
| 运输 |  工业 |  
| 食物饮料和烟草行业 |    消费者日常用品 |  
| 食物和必需品零售业 |    消费者日常用品 |  
| 家庭和个人用品 | 消费者日常用品 |  
| 媒体 | 非必需消费品 |  
| 汽车及配件 |  非必需消费品 |  
| 耐用消费品和服装 |非必需消费品 |  
| 消费性服务 |   非必需消费品 |  
| 零售业 | 非必需消费品 |  
| 医药业   | 健康保健 |  
| 卫生保健设备与服务 |    健康保健 |  
| 软件服务 | 信息技术 |  
| 技术硬件和设备   | 信息技术 |  
| 电信服务 |信息技术 |  
  
### <a name="see-also"></a>另请参阅  
- [为 Reporting Services 移动报表准备 Excel 数据](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)  
- [保留移动报表中 Analysis Services 数据的日期格式](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md)
- [使用 SQL Server 移动报表发布服务器创建移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
  
  

