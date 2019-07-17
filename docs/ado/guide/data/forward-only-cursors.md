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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925309"
---
# <a name="forward-only-cursors"></a>只进游标
典型的默认游标类型，称为只进 （或非可滚动） 游标中，可以仅向前移动的结果集。 只进游标不支持滚动 （向前和向后移动结果集中的功能）;它仅支持从一开始的行提取到结果集的末尾。 与某些只进游标 (如与 SQL Server 游标库)，则所有 insert、 update 和 delete 语句所做的当前用户 （或由其他用户提交） 在结果集中的影响行是可见的因为在提取行。 由于游标无法向后滚动，但是，在提取行后对数据库中的行进行的更改通过游标均不可见。  
  
 当前行的数据处理后，只进游标释放的资源，用来存放该数据。 默认只进游标是动态的，这意味着处理当前行时会检测到所有更改。 这可实现更快速的游标打开，并使结果集能够显示对基础表所做的更新。  
  
 虽然只进游标不支持向后滚动，您的应用程序可以返回到结果集关闭并重新打开游标的开头。 这是使用较少的数据的有效方法。 或者，你的应用程序无法读取结果集一次、 缓存数据保存在本地，，然后浏览本地数据缓存。  
  
 如果你的应用程序不需要滚动浏览结果集，只进游标是开销的使用最小快速检索数据的最佳方式。 使用**adOpenForwardOnly CursorTypeEnum**以指示你想要使用在 ADO 中的只进游标。  
  
## <a name="see-also"></a>请参阅  
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [由键集游标](../../../ado/guide/data/keyset-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)
