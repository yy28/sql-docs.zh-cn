---
title: 查看聚合使用情况 （聚合设计向导） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.aggregationdesignwizard.reviewusage.f1
ms.assetid: 107ee872-3df2-4931-b56c-af11e38f6745
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5a26ea23dda5bba4813a9c5a99d797471124750d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126422"
---
# <a name="review-aggregation-usage-aggregation-design-wizard"></a>查看聚合使用情况（聚合设计向导）
  可以使用 **“查看聚合使用情况”** 页配置聚合使用情况设置。  
  
## <a name="options"></a>“常规”  
 **Default**  
 选择此选项可以将属性的聚合使用情况设置设置为默认设置。 通过使用此设置，设计器可以根据属性和维度的类型应用默认规则。  
  
 `Full`  
 选择此项可设置到该属性的聚合使用情况设置`Full`。 使用此设置后，多维数据集的每个聚合都必须包含此属性或属性链中较低的相关属性。 `Full`如果属性包含许多成员，则应避免聚合使用情况设置。 如果为多个属性或具有多个成员的属性指定了此设置，则此设置可能会以尺寸过大为由，阻止设计聚合。  
  
 **无**  
 选择此选项可以将属性的聚合使用情况设置设置为无。 使用此设置后，多维数据集的聚合中将不会包含此属性。  
  
 `Unrestricted`  
 选择此项可设置到该属性的聚合使用情况设置`Unrestricted`。 使用此设置后，聚合设计器将不会受到任何限制，但是仍必须估算属性以确定它是否是一个有价值的聚合候选项。  
  
 **设置所有为默认值**  
 选择此选项可以将所有属性的聚合使用情况设置设置为默认设置。  
  
## <a name="see-also"></a>请参阅  
 [聚合设计向导的 F1 帮助](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 向导&#40;多维数据&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  