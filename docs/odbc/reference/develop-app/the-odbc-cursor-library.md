---
title: ODBC 游标库 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e1d6f7c6e532622d8bd0ee8fb637754f5df19429
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="the-odbc-cursor-library"></a>ODBC 游标库
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 块和可滚动游标是非常有用补充许多应用程序。 但是，并非所有驱动程序支持块和可滚动游标。 相同适用于定位更新和 delete 语句和**SQLSetPos**，其中论述了更新的数据。 因此，Windows SDK，以前包含在 Microsoft 数据访问组件 (MDAC) SDK，ODBC 组件包括游标库。 游标库实现块、 静态游标、 定位的更新和 delete 语句和**SQLSetPos**满足打开组标准 CLI 一致性级别任何驱动程序。 游标库可能与 ODBC 应用程序一起重新分发查看许可协议中的 SDK 的详细信息。  
  
 若要使用的是光标库，应用程序设置之后才会连接到数据源 SQL_ATTR_ODBC_CURSORS 连接属性。 游标库有关的详细信息，请参阅[附录 f: ODBC 游标库](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。
