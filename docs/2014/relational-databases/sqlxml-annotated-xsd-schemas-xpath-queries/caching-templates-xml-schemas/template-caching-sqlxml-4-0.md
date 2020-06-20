---
title: 模板缓存（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
author: rothja
ms.author: jroth
ms.openlocfilehash: 7a9e3025046dbb301ad192b02657db5e288cdaf7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85015810"
---
# <a name="template-caching-sqlxml-40"></a>模板缓存 (SQLXML 4.0)
  模板缓存极大地提高了性能。 如果设置模板缓存，该模板将在首次执行时保留在内存中。 这样可提高后续执行该模板的性能。  
  
 在注册表中添加以下项可以设置模板缓存大小：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 模板大小的设置应以可用内存和正在使用的模板数为基础。 **TemplateCacheSize**大小的默认值为31。 如果模板访问看起来较慢，您可以增加缓存大小；如果内存较少，则可以降低缓存大小。  
  
 为了获得更好的性能，建议您将**TemplateCacheSize**设置为高于通常使用的模板数。 如果**TemlateCacheSize**小于模板的数量，则性能会随模板数量的增加而降低。 **TemplateCacheSize**最大可以设置为128。  
  
 每次使用缓存的模板时，将检查模板文件的修改时间以确定是否需要刷新该模板。 其原因在于磁盘副本新于缓存副本。  
  
> [!NOTE]  
>  不能缓存模板参数和命令属性。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SQLXML 4.0&#41;的架构缓存](schema-caching-sqlxml-4-0.md)   
 [XSL 缓存 &#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  
