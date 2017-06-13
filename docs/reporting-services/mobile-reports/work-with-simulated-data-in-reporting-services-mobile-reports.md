---
title: "使用 Reporting Services 移动报表中的模拟数据 |Microsoft 文档"
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
ms.assetid: 6baabc36-58fb-4a98-bb9c-c42bafb16d0f
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0eb83717100f70933d2b1fe00bcd19a8a2901f65
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="work-with-simulated-data-in-reporting-services-mobile-reports"></a>Work with simulated data in Reporting Services mobile reports
将库元素放在设计图面上时， [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 会立即生成该元素的模拟数据。 创建移动报表时，此数据有许多用处。   
  
![SS_MRP_SimDataTreeMapProps](../../reporting-services/mobile-reports/media/ss-mrp-simdatatreemapprops.png)  
  
采用基于设计的方法创建移动报表时，模拟数据很有用。 最初使用模拟数据填充元素可以快速创建移动报表原型，而无需满足特定的数据要求。 然后就可以对这些移动报表的整体美感和有效性进行评估。  
  
## <a name="create-an-excel-file-with-simulated-data-as-a-template"></a>使用作为模板的模拟数据创建 Excel 文件  
  
模拟数据还提供了模板，该模板可以准确表示特定移动报表设计的数据要求。   
  
-  单击数据视图右上角的“导出所有数据”。   
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 生成包含模拟数据的 Excel 文档，从而能够快速替换成实际数据，以便进行导入。   
  
## <a name="how-simulated-data-behaves"></a>模拟数据的行为方式  
  
生成的模拟数据专门为你创建的移动报表量身定做。 放在设计图面上的元素增多时，关联的模拟数据也会增加和变化，在缺乏真实数据时也可提供最佳体验。 这种演化可以确保在将额外序列添加到图表可视化时，或者在以其他方式扩展一个或多个移动报表元素的范围时，额外字段和筛选可能项都可用。  
  
正如前面提到的，你可以将模拟数据导出到 Excel 文件，为关联移动报表创建一个完美的数据模板。 你可以将自己的真实数据替换到 Excel 文件中，并将其导回 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]。   
  
所有控件都绑定到真实数据之后，不再使用的模拟数据会自动从移动报表中删除。 不能删除设计图面上元素还在引用的模拟表。  
  
>**注意**：模拟数据不会添加到整个移动报表足迹，因为它没有使用移动报表进行序列化，而是在运行时实时生成。  
  
### <a name="see-also"></a>另请参阅  
- [使用 SQL Server 移动报表发布服务创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [在 iPad 应用中查看 SQL Server 移动报表和 KPI](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI for iOS)  
-  [View SQL Server mobile reports and KPIs in the iPhone app (Power BI for iOS)（在 iPhone 应用 (Power BI for iOS) 中查看 SQL Server 移动报表和 KPI）](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports)  
  
  
  
  
  


