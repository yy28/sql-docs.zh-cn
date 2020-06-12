---
title: 定义事实关系和事实关系属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 15f67a4bdf699bbc6443fc76ce54bcfb35831827
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547089"
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>定义事实关系和事实关系属性
  在定义新的多维数据集维度或新的度量值组时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将试图检测是否存在事实维度关系，然后将维度用法设置为 `Fact`。 您可以在多维数据集设计器的 **“维度用法”** 选项卡中查看或编辑事实维度关系。 维度与度量值组之间的事实关系具有以下约束：  
  
-   一个多维数据集维度与一个特定的度量值组只能具有一种事实关系。  
  
-   一个多维数据集维度可以与多个度量值组分别具有单独的事实关系。  
  
-   关系的粒度属性必须是维度的键属性（例如事务号）。 这将在维度和事实数据表中的事实之间创建一对一的关系。  
  
  
