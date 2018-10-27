---
title: 管理缓存 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d4d95e556059709f1d4e5a0fc069b6da5ed289c
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146543"
---
# <a name="managing-caches-xmla"></a>管理缓存 (XMLA)
  可以使用[ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla)命令，在 XML for Analysis (XMLA) 清除指定的维度或分区的缓存。 清除缓存可强制[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]重新生成该对象的缓存。  
  
## <a name="specifying-objects"></a>指定对象  
 [对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)属性的`ClearCache`命令可以包含仅对以下对象之一的对象引用。 如果包含的不是以下对象之一的对象引用，则会出错。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
