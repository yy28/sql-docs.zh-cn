---
title: 查看聚合使用情况 （聚合设计向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.aggregationdesignwizard.reviewusage.f1
ms.assetid: 107ee872-3df2-4931-b56c-af11e38f6745
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 10968a24c858f2523ff8b816bf153b9dc5dc2a8a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748279"
---
# <a name="review-aggregation-usage-aggregation-design-wizard"></a>查看聚合使用情况（聚合设计向导）
  可以使用 **“查看聚合使用情况”** 页配置聚合使用情况设置。  
  
## <a name="options"></a>选项  
 **默认**  
 选择此选项可以将属性的聚合使用情况设置设置为默认设置。 通过使用此设置，设计器可以根据属性和维度的类型应用默认规则。  
  
 `Full`  
 选择此选项可以将属性的聚合使用情况设置设置为 `Full`。 使用此设置后，多维数据集的每个聚合都必须包含此属性或属性链中较低的相关属性。 如果属性包含有多个成员，则应避免使用 `Full` 聚合使用情况设置。 如果为多个属性或具有多个成员的属性指定了此设置，则此设置可能会以尺寸过大为由，阻止设计聚合。  
  
 **无**  
 选择此选项可以将属性的聚合使用情况设置设置为无。 使用此设置后，多维数据集的聚合中将不会包含此属性。  
  
 `Unrestricted`  
 选择此选项可以将属性的聚合使用情况设置设置为 `Unrestricted`。 使用此设置后，聚合设计器将不会受到任何限制，但是仍必须估算属性以确定它是否是一个有价值的聚合候选项。  
  
 **全部设为默认值**  
 选择此选项可以将所有属性的聚合使用情况设置设置为默认设置。  
  
## <a name="see-also"></a>请参阅  
 [聚合设计向导的 F1 帮助](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 向导&#40;多维数据&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
