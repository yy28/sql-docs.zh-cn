---
title: 指定查询条件 （基于使用情况的优化向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.specifyquerycriteria.f1
ms.assetid: 3193adc2-af9f-4234-a4cc-dea0c280a724
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 088d53d1257c4b0d4b141b1e090ab1174416d397
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088377"
---
# <a name="specify-query-criteria-usage-based-optimization-wizard"></a>指定查询条件（基于使用情况的优化向导）
  可以使用 **“指定查询条件”** 页，选择一个或多个筛选器选项以指定要优化的查询。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 无法连接到查询日志，则将禁用此页。  
  
## <a name="options"></a>选项  
 **查询日志统计信息**  
 显示有关在所选分区的查询日志中所存储查询的信息。 将显示以下项：  
  
|术语|定义|  
|----------|----------------|  
|**总查询数**|显示在所选分区的查询日志中所存储查询的总数。|  
|**不同查询**|显示在所选分区的查询日志中所存储的不同查询数。|  
|**非重复用户**|显示与在所选分区的查询日志中所存储查询关联的不同用户总数。|  
|**平均响应时间**|显示在所选分区的查询日志中所存储查的平均响应时间。|  
  
 **开始日期**  
 基于开始日期和时间对查询日志中的查询进行筛选。 在下拉列表中选择或键入日期。  
  
> [!NOTE]  
>  如果未选择“结束日期”，则将对查询日志中此选项指定日期和时间之后（包括该日期）的所有查询进行筛选。  
  
 **结束日期**  
 基于结束日期和时间对查询日志中的查询进行筛选。 在下拉列表中选择或键入日期。  
  
> [!NOTE]  
>  如果未选择“开始日期”，则将对查询日志中此选项指定日期和时间之前（包括该日期）的所有查询进行筛选。  
  
 **用户**  
 基于指定的用户集对查询日志中的查询进行筛选。 单击省略号按钮 (**...**) 可以显示“用户选择”对话框，并选择要对其筛选查询的用户。 有关“用户选择”对话框的详细信息，请参阅[“用户选择”对话框（Analysis Services - 多维数据）](user-selection-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **最常见的查询**  
 基于对所选分区运行最为频繁的不同查询所占的百分比，对查询日志中的查询进行筛选。 在文本框中选择或键入一个百分比值。  
  
## <a name="see-also"></a>请参阅  
 [基于使用情况的优化向导的 F1 帮助](usage-based-optimization-wizard-f1-help.md)   
 [Analysis Services 向导&#40;多维数据&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
