---
title: 行为变化和 ODBC 3.x 驱动程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8343573261d74a6a0c652cf425b12da91f7cb0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292361"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>行为更改和 ODBC 3.x 驱动程序
环境属性SQL_ATTR_ODBC_VERSION向驱动程序指示是否需要显示 ODBC *2.x*行为还是 ODBC *3.x*行为。 SQL_ATTR_ODBC_VERSION环境属性的设置方式取决于应用程序。 ODBC *3.x*应用程序在调用**SQLAllocHandle**以分配环境句柄之前，在调用**SQLAllocHandle**以分配连接句柄之前，必须调用**SQLSetEnvAttr**来设置此属性。 如果他们未能执行此操作，驱动程序管理器将在后者调用**SQLAllocHandle**时返回 SQLSTATE HY010（函数序列错误）。  
  
> [!NOTE]  
>  有关行为更改和应用程序行为方式的详细信息，请参阅[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 ODBC *2.x*应用程序和 ODBC *2.x*应用程序使用 ODBC *3.x*标头文件重新编译，不调用**SQLSetEnvAttr**。 但是，他们调用**SQLAllocEnv**而不是**SQLAllocHandle**来分配环境句柄。 因此，当应用程序在驱动程序管理器中调用**SQLAllocEnv**时，驱动程序管理器在驱动程序中调用**SQLAllocHandle**和**SQLSetEnvAttr。** 因此，ODBC *3.x*驱动程序始终可以依赖于正在设置此属性。  
  
 如果使用ODBC_STD编译标志编译的符合标准的应用程序调用**SQLAllocEnv（** 这可能是由于**SQLAllocEnv**在 ISO 中未弃用而发生的），则调用在编译时映射到**SQLAllocHandleStd。** 在运行时，应用程序调用**SQLAllocHandleStd**。 驱动程序管理器将SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC3。 对**SQLAllocHandleStd**的调用等效于对**SQLAllocHandle**的调用，该调用具有SQL_HANDLE_ENV*的句柄类型*，以及对**SQLSetEnvAttr**的调用，以将SQL_ATTR_ODBC_VERSION设置为SQL_OV_ODBC3。  
  
 在某些驱动程序体系结构中，驱动程序需要显示为 ODBC *2.x*驱动程序或 ODBC *3.x*驱动程序，具体取决于连接。 在这种情况下，驱动程序实际上可能不是驱动程序，而是位于驱动程序管理器和另一个驱动程序之间的层。 例如，它可能模仿驱动程序，如 ODBC 间谍。 在另一个示例中，它可能充当网关，如 EDA/SQL。 要显示为 ODBC *3.x*驱动程序，此类驱动程序必须能够导出**SQLAllocHandle，** 并且要显示为 ODBC *2.x*驱动程序，必须能够导出**SQLAllocConnect、SQLAllocEnv**和**SQLAllocStmt**。 **SQLAllocEnv** 分配环境、连接或语句时，驱动程序管理器将检查此驱动程序是否导出**SQLAllocHandle**。 由于驱动程序确实如此，驱动程序管理器在驱动程序中调用**SQLAllocHandle。** 如果驱动程序使用 ODBC *2.x*驱动程序，则驱动程序必须根据需要将呼叫映射到**SQLAllocHandle、SQLAllocEnv**或**SQLAllocStmt。** **SQLAllocHandle** **SQLAllocEnv** 当作为 ODBC *2.x*驱动程序执行时，它还必须对**SQLSetEnvAttr**调用执行任何操作。  
  
 本部分包含以下主题。  
  
-   [日期时间数据类型](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 数据类型的后向兼容性](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [定长书签](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 支持](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [返回 SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [调用 SQLSetPos 以插入数据](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [按序号加载](../../../odbc/reference/appendixes/loading-by-ordinal.md)
