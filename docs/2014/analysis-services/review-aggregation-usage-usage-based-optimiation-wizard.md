---
title: 查看聚合使用情况 （基于使用情况的优化向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.reviewaggregationusage.f1
ms.assetid: 49ce2094-c4dc-4e46-8cef-c17c5db084ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a50c241bc70d48577b558827a278d5423ee8344b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164047"
---
# <a name="review-aggregation-usage-usage-based-optimiation-wizard"></a>查看聚合使用情况（基于使用情况的优化向导）
  可以使用 **“查看聚合使用情况”** 页配置聚合使用情况设置。  
  
## <a name="options"></a>选项  
 **Default**  
 选择此选项可以将属性的聚合使用情况设置设置为默认设置。 通过使用此设置，设计器可以根据属性和维度的类型应用默认规则。  
  
 **Full**  
 选择此选项可以将属性的聚合使用情况设置设置为完全。 使用此设置后，多维数据集的每个聚合都必须包含此属性或属性链中较低的相关属性。 如果属性包含有多个成员，则应避免使用 Full 聚合使用情况设置。 如果为多个属性或具有多个成员的属性指定了此设置，则此设置可能会以尺寸过大为由，阻止设计聚合。  
  
 **无**  
 选择此选项可以将属性的聚合使用情况设置设置为无。 使用此设置后，多维数据集的聚合中将不会包含此属性。  
  
 **不受限制**  
 选择此选项可以将属性的聚合使用情况设置设置为无限制。 使用此设置后，聚合设计器将不会受到任何限制。 但是仍必须估算属性以确定它是否是一个有价值的聚合候选项。  
  
 **全部设为默认值**  
 选择此选项可以将所有属性的聚合使用情况设置设置为默认设置。  
  
## <a name="see-also"></a>请参阅  
 [聚合设计向导的 F1 帮助](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 向导&#40;多维数据&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
