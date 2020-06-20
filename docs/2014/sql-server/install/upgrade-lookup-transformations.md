---
title: 升级查找转换 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 74430ab1bed232b8d510a8c28a8a690d88d1f6ba
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85041646"
---
# <a name="upgrade-lookup-transformations"></a>升级查找转换
  当您从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 时，请考虑将该包修改为利用查找转换中的新功能。 该转换支持 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中的缓存类型和数据输出选项。 有关其他缓存和数据输出的详细信息，请参阅[查找转换](../../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
 在 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中，可用的缓存类型有完全缓存、部分缓存和不缓存。 在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中，可以通过配置查找转换来使用其中一种缓存类型。 有关如何实现部分缓存或没有缓存的详细信息，请参阅[在无缓存或部分缓存模式下实现查找](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)。 有关如何实现完全缓存的信息，请参阅[在完全缓存模式下使用缓存连接管理器实现查找转换](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)，并[使用 OLE DB 连接管理器在完全缓存模式下实现查找转换](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)。  
  
 在 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中，查找转换具有一个输入、一个输出和一个错误输出。 在引用数据集中有匹配条目的输入中的行由输出处理。 没有匹配条目的输入中的行则被视为错误，并可能被重定向到错误输出。 在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中，查找转换有两个输出：匹配输出和不匹配输出。  
  
 默认情况下，当运行在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中创建的查找转换时，[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 将没有匹配条目的行视为错误，并允许您将这些行重定向到错误输出。 您也可以配置查找转换，以便将这些行视为非错误并将它们重定向到不匹配输出。  
  
 有关详细信息，请参阅[查找转换编辑器 &#40;常规页&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)。  
  
## <a name="see-also"></a>另请参阅  
 [查找转换](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
