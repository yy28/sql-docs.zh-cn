---
title: "扩展 OLAP 功能 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 49a17ff3-94e9-4969-84fc-37d49e63933b
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c41d406152efc89e097398d89c9a149dd6a5eb93
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="extending-olap-functionality"></a>扩展 OLAP 功能
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
作为一名程序员，您可以通过编写程序集、个性化扩展插件和存储过程来扩展 Analysis Services，以便提供您要在多个数据库应用程序中使用并重新确定其用途的功能。 程序集用于通过向 MDX 语言添加新的过程和函数或通过个性化外接程序来扩展多维模型功能。  
  
 存储过程可用于调用外部例程，并通过允许一次性开发常用代码并将其存储在单个位置来简化 Analysis Services 数据库的开发和实现。 存储过程可用来向应用程序中添加 MDX 的本机功能未提供的商业功能。  
  
 个性化设置是添加到多维数据集的自定义对象，可提供随用户的不同而不同的行为。 个性化设置并不是多维数据集中的永久对象，而是在用户会话期间客户端应用程序动态应用的对象。 例如，根据访问数据的人员更改货币值的币种、提供单个 KPI 或为网上购物的老客户提供针对性建议的列表。  
  
## <a name="in-this-section"></a>本節內容  
 [通过个性化设置扩展 OLAP](../../../analysis-services/multidimensional-models/extending-olap/extending-olap-through-personalizations.md)  
  
 [Analysis Services 个性化扩展](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
 [定义存储的过程](../../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
