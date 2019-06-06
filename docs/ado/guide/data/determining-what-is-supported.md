---
title: 确定支持的功能 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c6af51d8d69f5897021733468ee93290e1b5e280
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702095"
---
# <a name="determining-what-is-supported"></a>确定支持的功能
**支持**方法用于确定是否指定**记录集**对象支持特定类型的功能。 它具有以下语法：  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>备注  
 **支持**方法返回一个布尔值，该值指示是否提供程序支持所有由 CursorOptions 参数标识的功能。 可以使用**支持**方法来确定哪些类型的功能**记录集**对象支持。 如果**记录集**对象支持的功能，其相应的常量是*CursorOptions*，则**支持**方法将返回**True**. 否则，它将返回**False**。  
  
 使用**支持**方法，您可以检查的能力**记录集**对象添加新记录、 使用书签，请使用**查找**方法中，使用滚动时，使用**索引**属性，以及执行批处理更新。 常量及其含义的完整列表，请参阅[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)。  
  
 尽管**支持**方法可能会返回**True**对于给定的功能，它不保证，提供程序可以使该功能可在所有情况下。 **支持**方法仅返回满足某些条件的下提供程序是否支持指定的功能。 例如，**支持**方法可能指示**记录集**对象支持更新，即使游标基于多个表联接-其中某些列不是可更新。
