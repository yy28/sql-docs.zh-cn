---
title: 确定支持的功能 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 94c8f6c2f03fff3706f20982ac43237a52092bad
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="determining-what-is-supported"></a>确定支持的功能
**支持**方法用于确定是否指定**记录集**对象支持特定类型的功能。 它具有以下语法：  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>注释  
 **支持**方法返回一个布尔值，该值指示提供程序是否支持所有由 CursorOptions 参数标识的功能。 你可以使用**支持**方法来确定哪些类型的功能**记录集**对象支持。 如果**记录集**对象支持的功能，其相应常量位于*CursorOptions*、**支持**方法返回**True**. 否则，它将返回**False**。  
  
 使用**支持**方法，你可以检查的能力**记录集**对象添加新记录、 使用书签，请使用**查找**方法，请使用滚动，使用**索引**属性，并执行批处理更新。 常量和它们的含义的完整列表，请参阅[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)。  
  
 尽管**支持**方法可能返回**True**对于给定的功能，它无法保障，该提供程序可以使该功能可在所有情况下。 **支持**方法只返回满足某些条件的下提供程序是否支持指定的功能。 例如，**支持**方法可能表明**记录集**对象支持更新，即使光标基于多个表联接，其中某些列不是可更新。
