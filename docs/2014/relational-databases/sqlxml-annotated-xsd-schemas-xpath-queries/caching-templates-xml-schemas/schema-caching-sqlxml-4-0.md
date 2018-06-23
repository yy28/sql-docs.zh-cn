---
title: 架构缓存 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6ddf2b95f9b72a0def960f6159cd8646a6b4439c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026293"
---
# <a name="schema-caching-sqlxml-40"></a>架构缓存 (SQLXML 4.0)
  与通过并行安装的 Microsoft SQL Server 2000 Web 版本 1、 Microsoft SQLXML 2.0 和 SQLXML 3.0 的 XML，你可以显式控制缓存在所有版本中使用以下注册表项的架构：  
  
 Web Release 1：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 有关通过并行安装的详细信息，请参阅[What's New in SQLXML 4.0 SP1](../../sqlxml/what-s-new-in-sqlxml-4-0-sp1.md)。  
  
 架构缓存可极大提高 XPath 查询的性能。 对映射架构执行 XPath 查询时，架构存储在内存中，并且在内存中生成所需的数据结构。 如果设置了架构缓存，架构将保留在内存中，因此可提高后续 XPath 查询的性能。  
  
 可以通过在注册表中添加以上注册表项来设置架构缓存大小。  
  
 应基于可用内存大小和要使用的架构数量来设置架构缓存大小。 默认值**SchemaCacheSize**大小为 31。 如果你设置**SchemaCacheSize**更高版本，使用更多内存。 因此，如果架构访问较慢，可以增加缓存大小；如果内存较少，则可以降低缓存大小。  
  
 出于性能原因，建议你设置**SchemaCacheSize**高于您通常使用的映射架构的数。 当架构数目增加时，如果**SchemaCacheSize**小于比架构必须数，在性能降低。  
  
> [!NOTE]  
>  在开发期间，建议不缓存架构，因为这样会使对架构的更改在大约两分钟后才会反映在缓存中。  
  
## <a name="see-also"></a>请参阅  
 [模板缓存&#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [XSL 缓存&#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  