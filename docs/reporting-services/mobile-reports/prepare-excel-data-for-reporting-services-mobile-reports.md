---
title: "为 Reporting Services 移动报表准备 Excel 数据 | Microsoft Docs"
ms.custom: 
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16698f8d-bfc7-4eca-9e97-82c99d8bc08e
caps.latest.revision: "14"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b9f739a009fe8b80ce5005e8145b3fd95648e6f9
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="prepare-excel-data-for-reporting-services-mobile-reports"></a>为 Reporting Services 移动报表准备 Excel 数据
  
以下是准备移动报表要使用的 Excel 文件和工作表时，需要注意的一些事项︰  
  
## <a name="do"></a>要求事项  
  
- 每个数据集有一个工作表。  
- 第一行包含列标题。  
- 每一列的数据类型保持一致。  
- 将 Excel 中单元格的格式设置为合适类型。  
- 数据存放在工作表中，而不是在 Excel 的数据模型中。  
- 在使用公式时，请确保使用相同的公式计算整个列。  
- 使用 Excel 2007 或更高版本。  
- 用扩展名 XLSX 保存 Excel 文件。  
          
## <a name="dont"></a>禁止事项  
  
- 在数据集工作表中包含图像、图表、数据透视表或其他嵌入对象。  
- 包含总计或计算的行。  
- 导入时在文件已在 Excel 中打开。  
- 通过添加货币或其他符号手动设置数字格式。  
- 使用的工作簿包含在数据模型中存储的数据。  
  
## <a name="worksheets"></a>工作表  
          
在为移动报表准备作为数据集的 Excel 文件时，请确保每个工作表只能有一个数据集。 每个单独的工作表作为一个独立的表导入到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 。 导入后，将对具有相同名称的来自多个 Excel 源的工作表进行重命名，方法是在名称后追加递增的数字。 例如，如果工作簿具有三个标题为“MyWorksheet”的工作表，则第二个和第三个将被重命名为“MyWorksheet0”和“MyWorksheet1”。 下面的屏幕快照说明了可供导入的理想 Excel 工作表的前几行。  
  
![SS_MRP_ExcelDataSheet](../../reporting-services/mobile-reports/media/ss-mrp-exceldatasheet.png)  
          
## <a name="column-headers"></a>列标题  
  
正如在上面示例中看到的，第一行包含该列的标准名称。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 将保留这些列标题，以方便在库元素设置中引用。 但列标题并不是必需的。 如果缺少列标题， [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 将使用 Excel A、B、C、 …、AA、BB 等约定生成标题。  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]通过比较每一列中前两个单元格的数据类型，在导入 Excel 工作表时会自动检测第一行的标题。 如果任何列中前两个单元格的数据类型不匹配，则视为第一行包含列标题。 因此，如果表具有数值类型的列标题，请用字符串为标题名称加上前缀，以便在导入过程中将其检测为标题。  
  
## <a name="cells"></a>单元  
  
工作表数据集每一列中的单元数据应保持一致。 导入后，会为每一列分配数据类型。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 自动将数据类型检测为字符串、双精度（数值）、布尔值 (true/false) 或日期时间。 同一列中出现混合数据类型可能会导致检测不准确或完全失败。 此检测说明列标题可能为字符串类型。 应在 Excel 中正确设置单元格的类型，以确保 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 可以检测出所需的类型。 在上面的示例中，检测出六列的类型为︰  
*  日期时间列  
*  字符串列  
*  四个双精度列  
  
如果某个工作表包含计算的单元格或公式，则仅将生成的显示值导入到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]。  
  
## <a name="file-location-and-refreshing-excel-data"></a>文件位置和 Excel 数据刷新  
  
对于导入到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]中的 Excel 文件，其存储位置不受限制。 但是，如果在导入后移动或重命名该文件，将无法通过数据视图中的 **刷新所有数据** 命令来刷新该数据。   
  
>**注意**： [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 不会自动刷新 Excel 数据。 你可以通过 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] **刷新** 命令来刷新数据，但前提是文件没有移动。  
  
## <a name="dates"></a>日期  
  
日期字段对于许多移动报表都至关重要，因此应在 Excel 中将单元格的格式正确设置为日期。 在某些情况下，这意味着需要转换。 下面是一些公式示例，用于在 Excel 中将单元格从文本转换为日期。  
  
    Week 24-2013=DATE(MID(A2,9,4),1,-2)-WEEKDAY(DATE(MID(A2,9,4),1,3))+MID(A2,6,2)*7  
  
    2013/03/21=DATEVALUE(A1)  
  
    2013-mar-12=DATEVALUE(RIGHT(A1,2)&"-"&MID(A1,6,3)&"-"&LEFT(A1,4))  
  
转换单元格后，必须通过选择这些单元格，或从“类别”列表中依次选择整列 >“上下文”菜单 >“设置单元格格式” > “日期”来将其格式设置为日期。 还可以使用 Excel 文本分列向导将文本单元格转换为格式正确的日期。  
  
## <a name="unsupported"></a>不支持  
  
导入之后，以上述之外的格式保存的工作表数据可能会导致不可预知的结果。 它是在 Excel 文件中限制工作表格式的良策，可以将工作表设置为正确格式，以供移动报表使用。  
  
Excel 工作表中的自定义对象（包括数据透视表、可视化功能以及图像）不能导入到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]。  
  
### <a name="see-also"></a>另请参阅  
- [Prepare data for Reporting Services mobile reports](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)  
- [使用 SQL Server 移动报表发布服务创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [在 iPad 应用中查看 SQL Server 移动报表和 KPI](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI for iOS)  
-  [View SQL Server mobile reports and KPIs in the iPhone app (Power BI for iOS)（在 iPhone 应用 (Power BI for iOS) 中查看 SQL Server 移动报表和 KPI）](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports)  
  
  
  
  
  
  
  

