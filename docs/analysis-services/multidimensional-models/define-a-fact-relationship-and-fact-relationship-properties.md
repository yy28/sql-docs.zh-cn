---
title: "定义事实关系和事实关系属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c9ac99949cbac77b8a4edd806523acfc073c3dc2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>定义事实关系和事实关系属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在定义新的多维数据集维度或新的度量值组，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]将尝试检测是否存在事实维度关系，并将维度使用情况设置设置为**事实**。 您可以在多维数据集设计器的 **“维度用法”** 选项卡中查看或编辑事实维度关系。 维度与度量值组之间的事实关系具有以下约束：  
  
-   一个多维数据集维度与一个特定的度量值组只能具有一种事实关系。  
  
-   一个多维数据集维度可以与多个度量值组分别具有单独的事实关系。  
  
-   关系的粒度属性必须是维度的键属性（例如事务号）。 这将在维度和事实数据表中的事实之间创建一对一的关系。  
  
  
