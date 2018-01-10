---
title: "保留移动报表中 Analysis Services 数据的日期格式 | Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9a9a199-40e3-4381-b250-1b99fb83aa62
caps.latest.revision: "3"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a20327b51bd4fa05baa140bd8958dd9ff5486291
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="retain-date-formatting-for-analysis-services-in-mobile-reports"></a>保留移动报表中 Analysis Services 数据的日期格式
在报表生成器中为共享数据集添加一个度量值，以使 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 数据源中的数据在 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]中仍保留其数据类型。

[!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 查询的默认返回类型是一个字符串。  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 报表生成器中生成数据集时，将遵从该字符串类型，并且该字符串将保存到服务器。 

但是，当 JSON 表呈现器处理数据集时，它会按字符串读取列的值，并呈现字符串。  然后， [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] 提取表时，它也只会看到字符串。

关于此问题的解决方案是，当在报表生成器中创建共享数据集时，请添加一个计算成员。 它对 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 多维和表格模型均适用。

## <a name="create-a-measure-to-retain-a-date-field-data-type"></a>创建一个度量值以保留一个数据字段数据类型

1. 创建一个度量值以保存有问题的数据字段的值，在表达式字段中选择数据的层次结构/等级并附加 **.CurrentMember.MemberValue**。 例如：
 
   [Internet Sales].[Ship Date].CurrentMember.MemberValue
   
   ![ssas-calculated-member-report-builder](../../reporting-services/mobile-reports/media/ssas-calculated-member-report-builder.png)
   
2. 通过从左下角的“计算成员”列表将此计算成员拖动到右侧列网格中，可以将其附加到列集。  

   ![ssas-query-designer-calculated-member-report-builder](../../reporting-services/mobile-reports/media/ssas-query-designer-calculated-member-report-builder.png) 
   
### <a name="see-also"></a>另请参阅

-  [Data for Reporting Services mobile reports](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)
-  [为 Reporting Services 移动报表准备数据](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
