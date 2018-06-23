---
title: 管理缓存 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b40efd25088e90b3761d3532188d5bdadce7630c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128653"
---
# <a name="managing-caches-xmla"></a>管理缓存 (XMLA)
  你可以使用[ClearCache](../xmla/xml-elements-commands/clearcache-element-xmla.md)命令 XML 用于 Analysis (XMLA) 以清除指定的维度或分区的缓存中。 清除缓存强制[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]重新生成该对象的缓存。  
  
## <a name="specifying-objects"></a>指定对象  
 [对象](../xmla/xml-elements-properties/object-element-xmla.md)属性`ClearCache`命令都可以包含仅对以下对象之一的对象引用。 如果包含的不是以下对象之一的对象引用，则会出错。  
  
 “数据库”  
 清除数据库中包含的所有维度和分区的缓存。  
  
 维度  
 清除指定维度的缓存。  
  
 多维数据集  
 清除多维数据集的度量值组中包含的所有分区的缓存。  
  
 度量值组  
 清除度量值组中包含的所有分区的缓存。  
  
 分区  
 清除指定分区的缓存。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  