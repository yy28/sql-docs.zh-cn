---
title: OLE DB 的 Microsoft 游标服务 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aeac8c848f01f01e8969f94c571ad15f5e7f615a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923910"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>用于 OLE DB 的 Microsoft 游标服务
当你选择的客户端游标，或设置**CursorLocation**属性设置为**adUseClient**，用于 OLE DB 调用 Microsoft 游标服务。 您可能还会看到对"客户端游标引擎"，这是 ADO 的上下文中实质上是相同的操作的引用。 此服务对数据访问接口的游标支持函数进行了补充。 因此，您就可以理解来自所有数据提供程序相对统一的功能。  
  
 用于 OLE DB 游标服务使动态属性可用，增强了某些方法的行为。 例如，**优化**动态属性允许创建临时索引以简化某些操作，如**查找**方法。  
  
 游标服务支持批处理更新在所有情况下。 此外可以在数据访问接口仅提供性能较差的游标，如静态游标时模拟功能更强大的游标类型，如动态游标。  
  
## <a name="see-also"></a>请参阅  
 [用于 OLE DB （ADO 服务组件） 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
