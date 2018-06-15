---
title: 在 XML 中的记录集动态属性 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd874d0db6d026b82ddbc8055a17a073194c6e07
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272326"
---
# <a name="recordset-dynamic-properties-in-xml"></a>在 XML 中的记录集动态属性
当前，以下的记录集提供程序特定属性 （从客户端游标引擎） 被保存到 XML 格式：  
  
-   更新重新同步  
  
-   唯一表  
  
-   唯一的架构  
  
-   唯一的目录  
  
-   重新同步命令  
  
-   IrowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   重新调整形状名称  
  
-   AutoRecalc  
  
 作为保留的记录集的元素定义的特性，可将这些属性保存在架构部分。 这些属性在行集架构命名空间中定义，并且必须具有前缀"rs:"。  
  
## <a name="see-also"></a>请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
