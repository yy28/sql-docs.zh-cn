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
manager: craigg
ms.openlocfilehash: 471a65cb8f7560b409e6ddf8f73969d83d42a346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075786"
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>定义事实关系和事实关系属性
  在定义新的多维数据集维度或新的度量值组时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将试图检测是否存在事实维度关系，然后将维度用法设置为 `Fact`。 您可以在多维数据集设计器的 **“维度用法”** 选项卡中查看或编辑事实维度关系。 维度与度量值组之间的事实关系具有以下约束：  
  
-   一个多维数据集维度与一个特定的度量值组只能具有一种事实关系。  
  
-   一个多维数据集维度可以与多个度量值组分别具有单独的事实关系。  
  
-   关系的粒度属性必须是维度的键属性（例如事务号）。 这将在维度和事实数据表中的事实之间创建一对一的关系。  
  
  
