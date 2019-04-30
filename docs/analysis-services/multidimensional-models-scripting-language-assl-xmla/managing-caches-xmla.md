---
title: 管理缓存 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1080db165770b414d15e4ffb43daf5466021a71a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262078"
---
# <a name="managing-caches-xmla"></a>管理缓存 (XMLA)
  可以使用[ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla)命令，在 XML for Analysis (XMLA) 清除指定的维度或分区的缓存。 清除缓存可强制[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]重新生成该对象的缓存。  
  
## <a name="specifying-objects"></a>指定对象  
 [对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)的属性**ClearCache**命令可以包含仅对以下对象之一的对象引用。 如果包含的不是以下对象之一的对象引用，则会出错。  
  
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
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
