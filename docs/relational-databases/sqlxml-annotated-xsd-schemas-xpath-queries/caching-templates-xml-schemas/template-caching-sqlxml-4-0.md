---
title: "缓存 (SQLXML 4.0) 的模板 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0be646f13db19d52a71b248bf3a97f3ae60f5051
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="template-caching-sqlxml-40"></a>模板缓存 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]模板缓存可显著提高性能。 如果设置模板缓存，该模板将在首次执行时保留在内存中。 这样可提高后续执行该模板的性能。  
  
 在注册表中添加以下项可以设置模板缓存大小：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 模板大小的设置应以可用内存和正在使用的模板数为基础。 默认**TemplateCacheSize**大小为 31。 如果模板访问看起来较慢，您可以增加缓存大小；如果内存较少，则可以降低缓存大小。  
  
 为了提高性能，建议你设置**TemplateCacheSize**高于通常使用的模板数。 如果**TemlateCacheSize**小于比你有的模板数，性能下降的模板增加数。 **TemplateCacheSize**可以将设置为最多为 128。  
  
 每次使用缓存的模板时，将检查模板文件的修改时间以确定是否需要刷新该模板。 其原因在于磁盘副本新于缓存副本。  
  
> [!NOTE]  
>  不能缓存模板参数和命令属性。  
  
## <a name="see-also"></a>另请参阅  
 [架构缓存 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)   
 [XSL 缓存 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
