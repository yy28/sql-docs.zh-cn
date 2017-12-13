---
title: "管理缓存 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6dad9f3bb8c577ea8fb975d4f8ba4eac054f0a3e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="managing-caches-xmla"></a>管理缓存 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]你可以使用[ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)命令 XML 用于 Analysis (XMLA) 以清除指定的维度或分区的缓存中。 清除缓存强制[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]重新生成该对象的缓存。  
  
## <a name="specifying-objects"></a>指定对象  
 [对象](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)属性**ClearCache**命令都可以包含仅对以下对象之一的对象引用。 如果包含的不是以下对象之一的对象引用，则会出错。  
  
 数据库  
 清除数据库中包含的所有维度和分区的缓存。  
  
 维度  
 清除指定维度的缓存。  
  
 多维数据集  
 清除多维数据集的度量值组中包含的所有分区的缓存。  
  
 度量值组  
 清除度量值组中包含的所有分区的缓存。  
  
 分区  
 清除指定分区的缓存。  
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
