---
title: '附录 f: ODBC 游标库 |Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c27845976651b0d68b91b6269a21d1cae3518df8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649585"
---
# <a name="appendix-f-odbc-cursor-library"></a>附录 F：ODBC 游标库
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 ODBC 游标库 (Odbccr32.dll) 级别 1 API 一致性级别遵守任何驱动程序支持块可滚动游标，并可以由开发人员提供其应用程序或驱动程序一起重新发布。 游标库还支持定位的更新和删除语句生成的结果集**选择**语句。 虽然它支持仅静态游标和只进游标，游标库满足许多应用程序的需求。 此外，它可以提供良好的性能，尤其是对于小型到中型结果集，并没有很好的游标支持的应用程序。  
  
 游标库是驱动程序管理器和驱动程序之间的动态链接库 (DLL)。 当应用程序调用一个函数时，驱动程序管理器中执行的函数或在指定的驱动程序中调用它的游标库调用的函数。 对于给定的连接，应用程序指定游标库是始终使用、 驱动程序不支持可滚动游标，如果使用或从未使用过。  
  
 游标库将显示为驱动程序的驱动程序管理器。 如果游标库位于驱动程序管理器和 ODBC 2 之间。*x*驱动程序，该游标库显示为 ODBC 2。*x*驱动程序。 如果游标库位于驱动程序管理器和 ODBC 3 之间 *.x*驱动程序，该游标库显示为 ODBC 3 *.x*驱动程序。 由游标库展示的行为取决于它在使用，除了绑定偏移量，这两个 ODBC 2 支持的驱动程序的版本。*x*和 ODBC 3。*x*驱动程序。  
  
 若要实现中的块游标**SQLFetch**和**SQLFetchScroll**，将重复调用游标库**SQLFetch**驱动程序中。 若要实现滚动，它将缓存在内存和磁盘文件中检索的数据。 应用程序请求的新行集，该游标库根据需要从驱动程序或缓存检索它。  
  
 若要实现定位的 update 和 delete 语句，该游标库构造**更新**或**删除**语句与**其中**子句，以指定的已缓存每个绑定列的行中的值。 当它执行定位的更新语句时，游标库更新其缓存中的行集缓冲区的值。  
  
 有关 ODBC 游标库的详细信息，请参阅本附录的以下部分：  
  
-   [使用 ODBC 游标库](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [执行定位更新和删除语句](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [游标库代码示例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [实现说明](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 游标库错误代码](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
