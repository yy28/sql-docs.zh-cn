---
title: 管理缓存 (XMLA) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a6644b7caff5da31261b115bfc5608823622260a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="managing-caches-xmla"></a>管理缓存 (XMLA)
  你可以使用[ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)命令 XML 用于 Analysis (XMLA) 以清除指定的维度或分区的缓存中。 清除缓存强制[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]重新生成该对象的缓存。  
  
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
 [使用 Analysis Services 中的 XMLA 进行开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
