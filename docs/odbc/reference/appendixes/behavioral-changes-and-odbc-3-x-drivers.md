---
title: 行为更改和 ODBC 3.x 驱动程序 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aafe3522cee4f857ae4f5437bec219245cbc88d5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>行为更改和 ODBC 3.x 驱动程序
环境属性 SQL_ATTR_ODBC_VERSION 指示驱动程序是否需要展示 ODBC 2。*x*行为或 ODBC 3 *.x*行为。 如何设置 SQL_ATTR_ODBC_VERSION 环境属性取决于应用程序。 ODBC 3 *.x*应用程序必须调用**SQLSetEnvAttr**设置此属性后它们调用**SQLAllocHandle**分配环境句柄并在它们调用之前**SQLAllocHandle**分配连接句柄。 如果他们未能这样做，驱动程序管理器将返回 SQLSTATE HY010 （函数序列错误） 在后一种调用**SQLAllocHandle**。  
  
> [!NOTE]  
>  行为更改和应用程序的处理方式的详细信息，请参阅[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 ODBC 2。*x*应用程序和 ODBC 2。*x*通过 ODBC 3 重新编译的应用程序 *.x*标头文件不调用**SQLSetEnvAttr**。 但是，它们调用**SQLAllocEnv**而不是**SQLAllocHandle**分配环境句柄。 因此，在应用程序调用**SQLAllocEnv**在驱动程序管理器中，驱动程序管理器调用**SQLAllocHandle**和**SQLSetEnvAttr**驱动程序中。 因此，ODBC 3 *.x*驱动程序都始终可以依靠设置此属性。  
  
 如果符合标准的应用程序编译使用 ODBC_STD 编译标志调用**SQLAllocEnv** (这可能会导致**SQLAllocEnv** ISO 中不推荐使用)，调用映射到**SQLAllocHandleStd**在编译时。 在运行时，应用程序调用**SQLAllocHandleStd**。 驱动程序管理器将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3。 调用**SQLAllocHandleStd**等效于调用**SQLAllocHandle**与*HandleType* SQL_HANDLE_ENV 和调用**SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 设置为 SQL_OV_ODBC3。  
  
 在某些驱动程序体系结构中，没有要显示为任一 ODBC 2 的驱动程序需要。*x*驱动程序或 ODBC 3 *.x*驱动程序，具体取决于连接。 该驱动程序在此情况下可能实际上不是驱动程序，但驻留驱动程序管理器和另一个驱动程序之间的层。 例如，它可能会模拟驱动程序，如 ODBC Spy。 在另一个示例中，它可能充当网关，类似 EDA/SQL。 若要显示为 ODBC 3 *.x*驱动程序，这些驱动程序必须能够导出**SQLAllocHandle**，并显示为 ODBC 2。*x*驱动程序，必须能够导出**SQLAllocConnect**， **SQLAllocEnv**，和**SQLAllocStmt**。 如果必须执行环境、 连接或语句，并将其分配驱动程序管理器检查以确定如果此驱动程序导出**SQLAllocHandle**。 原因是驱动程序，驱动程序管理器调用**SQLAllocHandle**驱动程序中。 如果该驱动程序使用 ODBC 2。*x*驱动程序，该驱动程序必须映射到调用**SQLAllocHandle**到**SQLAllocConnect**， **SQLAllocEnv**，或**SQLAllocStmt**适当。 它还必须执行任何操作**SQLSetEnvAttr** ODBC 2 正常运行时调用。*x*驱动程序。  
  
 本部分包含以下主题。  
  
-   [日期时间数据类型](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 数据类型的后向兼容性](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [定长书签](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 支持](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [返回 SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [调用 SQLSetPos 以插入数据](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [按序号加载](../../../odbc/reference/appendixes/loading-by-ordinal.md)
