---
title: 指定对象计数（聚合设计向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 305d9d79-d1ab-4704-a7b5-3283842b3996
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d616997d3764aad42691d9ef3c213d553b5f311
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068306"
---
# <a name="specify-object-counts-aggregation-design-wizard"></a>指定对象计数（聚合设计向导）
  可以使用 **“指定对象计数”** 页自动计算多维数据集中的对象计数，或者手动输入估计的计数。 聚合设计向导使用对象计数来估计存储要求。  
  
## <a name="options"></a>选项  
 **多维数据集对象**  
 显示多维数据集中的维度和属性。 仅显示在向导的 "**查看聚合使用情况**" `None`页中不将其`AggregationUsage`属性设置为的特性，因为只有这些特性需要指定计数。  
  
 **估计的计数**  
 显示度量值组中估计的行数和数据库维度中估计的属性成员计数。 您可以键入一个值，以用作估计的计数，或可以计算估计的计数值。 若要计算计数值，请`0`在字段中键入，然后单击 "**计数**"。 已显示计数的字段不会更新。  
  
 **分区计数**  
 （可选）键入度量值组中估计的行数和分区中估计的属性成员计数。  
  
 **Count**  
 计算并重新填充所有空字段的“估计的计数”**** 列。 已显示计数的字段不会更新。  
  
## <a name="see-also"></a>另请参阅  
 [聚合设计向导的 F1 帮助](aggregation-design-wizard-f1-help.md)   
 [&#40;多维数据的 Analysis Services 向导&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
