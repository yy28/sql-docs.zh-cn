---
title: XSL 缓存 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
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
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b95f2970c7d1d9848d6b58c4feaeb462c084d369
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028080"
---
# <a name="xsl-caching-sqlxml-40"></a>XSL 缓存 (SQLXML 4.0)
  缓存 XSL 样式表可提高性能。 如果 XSL 缓存设置为 ON，则在第一次执行之后，XSL 样式表将保留在内存中；这可以提高后续处理的性能。 默认设置为 ON。  
  
 通过在注册表中添加以下项可以设置 XSL 缓存大小：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 应根据可用内存和要使用的 XSL 样式表的个数来设置 XSL 缓存大小。 默认**XSLCacheSize**大小为 31。 如果 XSL 访问看起来较慢，您可以增加缓存大小；如果内存较少，则可以降低缓存大小。  
  
 为了提高性能，建议你设置**XSLCacheSize**高于您通常使用的 XSL 样式表数。 如果**XSLCacheSize**是小于的数字的 XSL 样式的表的在性能降低的 XSL 样式表增加数字的形式。 **XSLCacheSize**可以将设置为最多为 128。  
  
 每次使用缓存的 XSL 样式表时，都将检查 XSL 文件的修改时间以确定是否需要刷新该样式表。 其原因在于磁盘副本新于缓存副本。  
  
## <a name="see-also"></a>请参阅  
 [模板缓存&#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [架构缓存&#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
  
  