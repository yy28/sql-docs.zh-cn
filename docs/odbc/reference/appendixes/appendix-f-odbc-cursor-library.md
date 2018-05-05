---
title: '附录 f: ODBC 游标库 |Microsoft 文档'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10e43272c7d9a75956aa162398c2869c558cdea1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="appendix-f-odbc-cursor-library"></a>附录 f: ODBC 游标库
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 ODBC 游标库 (Odbccr32.dll) 以任何符合级别 1 API 一致性级别的驱动程序支持块可滚动游标，可以通过开发人员提供对其应用程序或驱动程序一起重新分发。 游标库还支持定位的更新和 delete 语句的结果集生成的**选择**语句。 尽管它支持仅静态和只进游标，游标库满足许多应用程序的需求。 此外，它可提供良好的性能，尤其是对于小型到中型结果集，以及应用程序不提供良好的游标支持。  
  
 游标库是动态链接库 (DLL) 位于之间驱动程序管理器和驱动程序。 当应用程序调用一个函数时，驱动程序管理器将调用中光标库，它执行的函数或在指定的驱动程序中调用它的函数。 对于给定的连接，应用程序指定的是光标库是始终使用，使用该驱动程序不支持可滚动游标，如果还是从未使用过。  
  
 游标库显示为驱动程序到驱动程序管理器。 如果游标库驻留驱动程序管理器和 ODBC 2 之间。*x*驱动程序，光标库显示为 ODBC 2。*x*驱动程序。 如果游标库所在驱动程序管理器和 ODBC 3 之间 *.x*驱动程序，光标库显示为 ODBC 3 *.x*驱动程序。 游标库的行为取决于它正在使用，除了绑定偏移量，这两个 ODBC 2 支持的驱动程序的版本。*x*和 ODBC 3。*x*驱动程序。  
  
 若要实现的块游标**SQLFetch**和**SQLFetchScroll**，反复调用的是光标库**SQLFetch**驱动程序中。 若要实现滚动，它将缓存检索到它在内存和磁盘文件中的数据。 当应用程序请求一个新行集时，游标库将检索它根据需要从该驱动程序或缓存。  
  
 若要实现定位的 update 和 delete 语句，光标库构造**更新**或**删除**语句**其中**子句，以指定的已缓存行中每个绑定列的值。 当它执行的定位的更新语句时，游标库将更新其缓存中的行集缓冲区中的值。  
  
 有关 ODBC 游标库的详细信息，请参阅本附录的以下各节：  
  
-   [使用 ODBC 游标库](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [执行定位更新和删除语句](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [游标库代码示例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [实现说明](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 游标库错误代码](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
