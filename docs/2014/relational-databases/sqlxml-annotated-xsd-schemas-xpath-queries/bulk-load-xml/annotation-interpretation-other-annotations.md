---
title: 其他批注 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fff698fc4eb92dd1bade50274a289f861e07ede0
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013613"
---
# <a name="other-annotations-sqlxml-40"></a>其他批注 (SQLXML 4.0)
  除本节上文的主题中介绍的批注之外，XML 大容量加载还解释了以下其他批注：  
  
 `sql:id-prefix`  
 如果架构为 XML 数据指定了前缀，XML 大容量加载在将这些数据发送到 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前会删除这些前缀。  
  
 `sql:use-cdata`  
 XML 大容量加载读取存储在 CDATA 部分中的文本，然后将其发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 `sql:url-encode`  
 XML 大容量加载不支持此批注。 例如，不能在 XML 数据输入中指定某一 URL 并期望大容量加载从该位置读取数据，以将其存储在数据库中。  
  
 `sql:is-mapping-schema`  
 XML 大容量加载不支持此批注，也不支持 `sql:id`。  
  
> [!NOTE]  
>  XML 大容量加载不支持内联映射架构。  
  
 `sql:key-fields`  
 XML 大容量加载始终忽略此批注。  
  
## <a name="see-also"></a>请参阅  
 [批注解释&#40;SQLXML 4.0&#41;](annotation-interpretation-sqlxml-4-0.md)  
  
  
