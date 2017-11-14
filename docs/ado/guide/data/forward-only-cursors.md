---
title: "只进游标 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 121e8eec0b95f66b6e034f1f77d78c7d88fd5184
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="forward-only-cursors"></a>只进游标
典型的默认游标类型，称为只进 （或非可滚动） 游标，可以仅向前移动结果集。 只进游标不支持滚动 （向前和向后移动结果集中的能力）;它仅支持从一开始的行提取到结果集的末尾。 与某些只进游标 (如与 SQL Server 光标库)，则所有 insert、 update 和 delete 语句所做的当前用户 （或由其他用户提交） 读取行时，在结果集中的影响行是否可见。 因为不能向后滚动光标，但是，提取行之后对数据库中的行所做的更改不会通过游标可见。  
  
 处理当前行的数据后，只进游标将释放用来存放该数据的资源。 只进游标默认为动态，这意味着处理当前行时检测到所有更改。 这提供了更快的游标打开，并使结果集以显示对基础表所做的更新。  
  
 尽管只进游标不支持向后滚动，你的应用程序可以返回到的结果集通过关闭并重新打开光标开头。 这是使用较少的数据的有效方式。 作为替代方法，你的应用程序无法读取一次的结果集，本地，缓存数据，然后浏览本地数据缓存。  
  
 如果你的应用程序不需要滚动浏览结果集，只进游标是开销的使用最小快速检索数据的最佳办法。 使用**adOpenForwardOnly CursorTypeEnum**以指示你想要使用在 ADO 的只进游标。  
  
## <a name="see-also"></a>另请参阅  
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [键集游标](../../../ado/guide/data/keyset-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)

