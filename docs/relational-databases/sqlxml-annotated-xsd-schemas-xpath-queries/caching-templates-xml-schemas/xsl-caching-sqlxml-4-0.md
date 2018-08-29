---
title: XSL 缓存 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ec64e136aedf80685c6484d52de336b1014a4ae8
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43084406"
---
# <a name="xsl-caching-sqlxml-40"></a>XSL 缓存 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  缓存 XSL 样式表可提高性能。 如果 XSL 缓存设置为 ON，则在第一次执行之后，XSL 样式表将保留在内存中；这可以提高后续处理的性能。 默认设置为 ON。  
  
 通过在注册表中添加以下项可以设置 XSL 缓存大小：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 应根据可用内存和要使用的 XSL 样式表的个数来设置 XSL 缓存大小。 默认值为**XSLCacheSize**大小为 31。 如果 XSL 访问看起来较慢，您可以增加缓存大小；如果内存较少，则可以降低缓存大小。  
  
 为了提高性能，建议您设置**XSLCacheSize**大于您通常使用的 XSL 样式表的数。 如果**XSLCacheSize**是小于的数字 XSL 样式的表的有，则性能会数目的 XSL 样式表增加。 **XSLCacheSize**可以设置为最多为 128。  
  
 每次使用缓存的 XSL 样式表时，都将检查 XSL 文件的修改时间以确定是否需要刷新该样式表。 其原因在于磁盘副本新于缓存副本。  
  
## <a name="see-also"></a>请参阅  
 [模板缓存&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [架构缓存&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  
