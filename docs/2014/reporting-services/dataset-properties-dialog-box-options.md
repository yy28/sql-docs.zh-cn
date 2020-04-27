---
title: "\"数据集属性\" 对话框-> \"选项\" |Microsoft Docs"
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10130"
- sql12.rtp.rptdesigner.datasetproperties.options.f1
ms.assetid: 95299049-71ba-427f-b723-775cb696243f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 778365e8fc7f40700b0f8c1683260f15c860a32a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109413"
---
# <a name="dataset-properties-dialog-box-options"></a>“数据集属性”对话框 -&gt;“选项”
  在 " **DatasetProperties** " 对话框中选择 "**选项**" 可更改查询的数据选项，如排序规则选项和小计。 有关详细信息，请参阅 [排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="options"></a>选项  
 **排序规则**  
 选择用于决定在对数据排序时所用的排序规则顺序的区域设置。 **“默认值”** 指示报表服务器在报表运行时将尝试从数据访问接口派生该值。 如果无法派生该值，则将从计算机的区域设置派生默认值。  
  
 **区分大小写**  
 选择一个用于决定是否区分大小写的值。 此选项指示数据是否区分大小写。 可以将**区分大小写**设置**为 True**、 **False**或**Auto**。默认值为 "**自动**"，指示 Report Server 应在报表运行时尝试从数据提供程序派生该值。 如果数据提供程序不支持区分大小写的类型，则报表将按该值为 **False**的情况运行。 如果您知道该值并且知道该值受支持，请选择 **True**。  
  
 **区分重音**  
 选择一个用于决定是否区分重音的值。 "**区分重音**" 指示数据是否区分重音; 可以将其设置为**True**、 **False**或 "**自动**"。默认值为 "**自动**"，指示在运行报表时，Report Server 应尝试从数据访问接口派生该值。 如果数据访问接口不支持区分重音的类型，则报表将按该值为 **False**的情况运行。 如果您知道该值并且知道该值受支持，请选择 **True**。  
  
 **区分假名类型**  
 选择一个用于决定是否区分假名类型的值。 此选项指示数据是否区分假名类型敏感;它可以设置为 " **True**"、" **False**" 或 "**自动**"。默认值为 "**自动**"，指示 Report Server 应在报表运行时尝试从数据提供程序派生该值。 如果数据访问接口不支持区分假名类型的类型，则报表将按该值为 **False**的情况运行。 如果您知道该值并且知道该值受支持，请选择 **True**。  
  
 **区分全半角**  
 选择一个用于决定是否区分全半角的值。 此选项指示数据是否区分全半角并可设置为**True**、 **False**或**Auto**。默认值为 "**自动**"，指示 Report Server 应在报表运行时尝试从数据提供程序派生该值。 如果数据访问接口不支持区分全半角的类型，则报表将按该值为 **False**的情况运行。 如果您知道该值并且知道该值受支持，请选择 **True**。  
  
 **将小计解释为详细信息行**  
 选择一个值，该值指示是否希望将小计行解释为详细信息行而非聚合行。 默认值为 "**自动**"，指示如果报表不使用`Aggregate`（）函数访问数据集中的任何字段，则应将小计行视为详细信息行。 如果希望将小计行解释为聚合行，请选择 **False**。 如果希望将小计行解释为详细信息行，并且知道它们不使用（）函数，请`Aggregate`选择 " **True**"。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表或文本框的区域设置 &#40;Reporting Services&#41;](report-design/set-the-locale-for-a-report-or-text-box-reporting-services.md)   
 [将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Windows 排序规则名称 (Transact-SQL)](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [SQL Server 排序规则名称 (Transact-SQL)](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [聚合函数（报表生成器和 SSRS）](report-design/report-builder-functions-aggregate-function.md)  
  
  
