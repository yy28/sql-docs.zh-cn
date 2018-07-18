---
title: “数据集属性”对话框 ->“选项”（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-data
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- "10020"
- sql13.rtp.rptdesigner.datasetproperties.options.f1
- "10130"
ms.assetid: 43e50133-45ef-47a2-b575-34dfcc28ec98
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 411fe1b3d55ec8ad34120fd69ee129910e75a6b0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33020744"
---
# <a name="dataset-properties-dialog-box-options-report-builder"></a>“数据集属性”对话框 -&gt;“选项”（报表生成器）
  在“数据集属性”对话框中选择“选项”可更改查询的数据选项，如排序规则选项和将小计视为详细数据进行处理。 有关排序规则的详细信息，请参阅 [SQL Server 联机丛书](../../relational-databases/collations/collation-and-unicode-support.md) 中的 [排序规则和 Unicode 支持](http://go.microsoft.com/fwlink/?linkid=98335)。  
  
 作为报表服务器上共享数据集定义一部分的数据选项会影响使用共享数据集的所有报表。 可以在将其添加到报表后覆盖共享数据集的选项。 这些更改只会影响定义它们的报表。  
  
 嵌入数据集的数据选项也只会影响定义它们的报表。  
  
 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>“常规”  
 **排序规则**  
 选择用于决定在对数据排序时所用的排序规则顺序的区域设置。 **“默认值”** 指示报表服务器在报表运行时将尝试从数据访问接口派生该值。 如果无法派生该值，则将从计算机的区域设置派生默认值。  
  
 **区分大小写**  
 选择一个用于决定是否区分大小写的值。 此选项指示数据是否区分大小写。 您可以将 **“区分大小写”** 设置为 **True**、 **False**或 **“自动”**。默认值为“自动”，指示报表服务器应在报表运行时尝试从数据提供程序派生该值。 如果数据提供程序不支持区分大小写的类型，则报表将按该值为 **False**的情况运行。 如果您知道该值并且知道该值受支持，请选择 **True**。  
  
 **区分重音**  
 选择一个用于决定是否区分重音的值。 **“区分重音”** 指示数据是否区分重音；可以将此选项设置为 **True**、 **False**或 **“自动”**。默认值为“自动”，指示报表服务器应在报表运行时尝试从数据提供程序派生该值。 如果数据访问接口不支持区分重音的类型，则报表将按该值为 **False**的情况运行。 如果您知道该值并且知道该值受支持，请选择 **True**。  
  
 **区分假名类型**  
 选择一个用于决定是否区分假名类型的值。 此选项指示数据是否区分假名类型；可以将此选项设置为 **True**、 **False**或 **“自动”**。默认值为“自动”，指示报表服务器应在报表运行时尝试从数据提供程序派生该值。 如果数据访问接口不支持区分假名类型的类型，则报表将按该值为 **False**的情况运行。 如果您知道该值并且知道该值受支持，请选择 **True**。  
  
 **区分全半角**  
 选择一个用于决定是否区分全半角的值。 此选项指示数据是否区分全半角；可设置为 True、False 或“自动”。默认值为“自动”，指示报表服务器应在报表运行时尝试从数据提供程序派生该值。 如果数据访问接口不支持区分全半角的类型，则报表将按该值为 **False**的情况运行。 如果您知道该值并且知道该值受支持，请选择 **True**。  
  
 **将小计解释为详细信息行**  
 选择一个值，该值指示是否希望将小计行解释为详细信息行而非聚合行。 默认值为“自动”，指示如果报表未使用 Aggregate() 函数来访问数据集中的任何字段，则应将小计行视为详细信息行。 如果希望将小计行解释为聚合行，请选择 **False**。 如果希望将小计行解释为详细信息行，并且知道它们不使用 Aggregate() 函数，请选择“True”。  
  
## <a name="see-also"></a>另请参阅  
 [用于对话框、窗格和向导的报表生成器帮助](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [聚合函数（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [“数据集属性”对话框 ->“查询”（报表生成器）](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md)  
  
  
