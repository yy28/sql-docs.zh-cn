---
title: "定义事实关系和事实关系属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0b86ebd4da388cbaf303bcdab92fe3fce3994fe1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>定义事实关系和事实关系属性
  在定义新的多维数据集维度或新的度量值组时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将试图检测是否存在事实维度关系，然后将维度用法设置为 **Fact**。 您可以在多维数据集设计器的 **“维度用法”** 选项卡中查看或编辑事实维度关系。 维度与度量值组之间的事实关系具有以下约束：  
  
-   一个多维数据集维度与一个特定的度量值组只能具有一种事实关系。  
  
-   一个多维数据集维度可以与多个度量值组分别具有单独的事实关系。  
  
-   关系的粒度属性必须是维度的键属性（例如事务号）。 这将在维度和事实数据表中的事实之间创建一对一的关系。  
  
  

