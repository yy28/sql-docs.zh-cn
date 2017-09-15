---
title: "用于 OLE DB Microsoft 游标服务 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce4deae8dc07c546fc777a6fa86d159b404c60f9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>用于 OLE DB Microsoft 游标服务
当你选择客户端游标，或设置**CursorLocation**属性**adUseClient**，正在对于 OLE DB 调用 Microsoft 游标服务。 你可能还会看到"客户端游标引擎"，这是实质上是相同的 ADO 的上下文中的引用。 此服务将补充数据提供程序的光标支持函数。 因此，您就可以理解相对统一的功能，从所有数据提供程序。  
  
 OLE DB 游标服务提供动态属性，并增强的某些方法的行为。 例如，**优化**动态属性允许创建临时索引，以便于某些操作，如**查找**方法。  
  
 游标服务能够在所有情况下更新批处理的支持。 它还可以模拟功能更强大的游标类型，如动态游标时数据提供程序可以仅提供能力较小的游标，如静态游标。  
  
## <a name="see-also"></a>另请参阅  
 [用于 OLE DB （ADO 服务组件） 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
