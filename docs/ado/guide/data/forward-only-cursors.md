---
title: 只进游标 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e84fbf2b8fda2fa2b14088af1e0830d8109aba8a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925309"
---
# <a name="forward-only-cursors"></a>只进游标
典型的默认游标类型称为只进（或不可滚动）游标，只能通过结果集向前移动。 只进游标不支持滚动（在结果集中向前和向后移动的能力）;它仅支持从结果集的开始处提取行。 对于某些只进游标（例如，使用 SQL Server 游标库），当前用户（或其他用户提交的）所做的所有 insert、update 和 delete 语句都将在提取行时可见。 由于游标无法向后滚动，但是，在提取行后对数据库中的行进行的更改通过游标均不可见。  
  
 处理当前行的数据后，只进游标将释放用于保存这些数据的资源。 默认只进游标是动态的，这意味着处理当前行时会检测到所有更改。 这可实现更快速的游标打开，并使结果集能够显示对基础表所做的更新。  
  
 当只进游标不支持向后滚动时，您的应用程序可以通过关闭和重新打开游标返回到结果集的开头。 这是使用少量数据的有效方法。 作为替代方法，应用程序可以读取结果集一次，将数据缓存在本地，然后浏览本地数据缓存。  
  
 如果您的应用程序不需要在结果集中滚动，则只进游标是使用最少的开销快速检索数据的最佳方式。 使用**AdOpenForwardOnly CursorTypeEnum**指示你希望在 ADO 中使用只进游标。  
  
## <a name="see-also"></a>另请参阅  
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [键集游标](../../../ado/guide/data/keyset-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)
