---
title: "Reporting Services 移动报表的数据 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91138ef8-ddb4-4ac5-a1e4-fa4cf1c58dcc
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fe007313e57ec01c5c456b0623b642555a25bf35
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="data-for-reporting-services-mobile-reports"></a>Reporting Services 移动报表的数据
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] 数据模型非常简单。 将数据作为数据集的集合导入 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 。 不需要数据集之间的正式关系。 只要键值匹配，就可以在各个数据集之间进行查找。 日期/时间聚合通过移动报表运行时进行处理，即使数据集之间的日期/时间数据粒度不同，它们也会在不同的数据集之间进行匹配。   
  
可以从以下两种类型的源导入数据：   
  
* **本地 Excel 文件**：选择 Excel 文档，然后选择要导入的工作表。 导入后，数据将存储在移动报表定义中。 若要刷新原始 Excel 文件中的数据，请使用 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]“数据”选项卡右上角的“刷新数据”命令。 阅读关于 [为 SSRS 移动报表准备 Excel 数据](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)的详细信息。  
  
* **[!INCLUDE[PRODUCT_NAME](../../includes/server-product-name.md)] 共享数据集**：浏览服务器上已发布数据集的列表，然后选择要添加到移动报表中的数据集。 基于服务器数据的移动报表始终与原始服务器数据集标尺连接，并反映该服务器上的数据的最新状态。 请参阅 [支持的数据源列表](https://msdn.microsoft.com/library/ms159219.aspx)。   
  
  阅读有关 [从移动报表发布服务器中的共享数据集获取数据](../../reporting-services/mobile-reports/get-data-from-shared-datasets-in-reporting-services-mobile-reports.md)的详细信息。  
  
将数据导入到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]之后，无论数据来自何处，其余移动报表创建和设计体验都完全相同。   
  
## <a name="connect-mobile-report-elements-to-data"></a>将移动报表元素连接到数据 ##  
  
每个 [!INCLUDE[PRODUCT_NAME](../../includes/short-product-name.md)] 元素都包含一个或多个数据设置。 例如，径向仪表元素包含两个数据设置：主值和比较值。 上述每个设置都精确指向特定数据集中一个字段（列）。   
  
移动报表运行时将根据用户选择为该仪表提供聚合值。 请注意，可以将同一个径向仪表实例的比较值从不同数据集绑定到一个字段。   
  
### <a name="see-also"></a>另请参阅  
-  [Prepare data for Reporting Services mobile reports](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
- [使用 SQL Server 移动报表发布服务创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
- [Get data from shared datasets](../../reporting-services/mobile-reports/get-data-from-shared-datasets-in-reporting-services-mobile-reports.md)
- [保留移动报表中 Analysis Services 数据的日期格式](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) 
  
  


