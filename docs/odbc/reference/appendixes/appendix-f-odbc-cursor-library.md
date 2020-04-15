---
title: 附录 F：ODBC 光标库 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec7982150bfa805c7093ab445400ef5ad1ee070c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292427"
---
# <a name="appendix-f-odbc-cursor-library"></a>附录 F：ODBC 游标库
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 ODBC 游标库 （Odbccr32.dll） 支持符合 1 级 API 符合性级别且开发人员可以使用其应用程序或驱动程序重新分发的任何驱动程序的可滚动游标。 游标库还支持**为 SELECT**语句生成的结果集定位更新和删除语句。 尽管它仅支持静态和仅转发游标，但游标库可满足许多应用程序的需求。 此外，它可以提供良好的性能，特别是对于中小型结果集，以及没有良好光标支持的应用程序。  
  
 游标库是位于驱动程序管理器和驱动程序之间的动态链接库 （DLL）。 当应用程序调用函数时，驱动程序管理器调用游标库中的函数，该库执行该函数或在指定的驱动程序中调用该函数。 对于给定的连接，应用程序指定是否始终使用游标库、驱动程序不支持可滚动游标或从未使用过。  
  
 光标库显示为驱动程序管理器的驱动程序。 如果光标库位于驱动程序管理器和 ODBC *2.x*驱动程序之间，则光标库将显示为 ODBC *2.x*驱动程序。 如果光标库位于驱动程序管理器和 ODBC *3.x*驱动程序之间，则光标库显示为 ODBC *3.x*驱动程序。 游标库显示的行为取决于它使用的驱动程序的版本，但绑定偏移量除外，ODBC *2.x*和 ODBC *3.x*驱动程序都支持该偏移量。  
  
 为了在**SQLFetch**和**SQLFetchScroll**中实现块游标，游标库在驱动程序中反复调用**SQLFetch。** 为了实现滚动，它缓存它在内存和磁盘文件中检索的数据。 当应用程序请求新的行集时，游标库根据需要从驱动程序或缓存中检索它。  
  
 要实现定位的更新和删除语句，游标库构造一个**更新**或**DELETE**语句，该语句具有**WHERE**子句，用于指定行中每个绑定列的缓存值。 当它执行定位的更新语句时，游标库会从行集缓冲区中的值更新其缓存。  
  
 有关 ODBC 游标库的详细信息，请参阅本附录的以下部分：  
  
-   [使用 ODBC 游标库](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [执行定位更新和删除语句](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [游标库代码示例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [实施说明](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 游标库错误代码](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
