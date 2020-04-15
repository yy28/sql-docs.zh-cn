---
title: 符合标准的应用程序和驱动程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b4daf2e777b20b1b84c090757d0d84796a4cae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299714"
---
# <a name="standards-compliant-applications-and-drivers"></a>符合标准的应用程序和驱动程序
符合标准的应用程序或驱动程序符合开放组 CAE 规范"数据管理：SQL 调用级接口 （CLI）"和 ISO/IEC 9075-3：1995 （E） 呼叫级接口 （SQL/CLI）。  
  
 ODBC *3.x*保证具有以下功能：  
  
-   写入 Open Group 和 ISO CLI 规范的应用程序在使用 ODBC *3.x*标头文件编译并与 ODBC *3.x*库链接时，以及通过 ODBC *3.x*驱动程序管理器访问驱动程序时，将使用 ODBC *3.x*驱动程序或符合标准的驱动程序。  
  
-   写入 Open Group 和 ISO CLI 规范的驱动程序在使用 ODBC *3.x*标头文件编译并与 ODBC *3.x*库链接时，以及当应用程序通过 ODBC *3.x*驱动程序管理器访问驱动程序时，它将与 ODBC *3.x*应用程序或符合标准的应用程序配合使用。  
  
 符合标准的应用程序和驱动程序使用ODBC_STD编译标志进行编译。  
  
 符合标准的应用程序表现出以下行为：  
  
-   如果符合标准的应用程序调用**SQLAllocEnv（** 这可能是因为**SQLAllocEnv**是 Open 组和 ISO CLI 中的有效函数，则调用将在编译时映射到**SQLAllocHandleStd。** 因此，在运行时，应用程序调用**SQLAllocHandleStd**。 在处理此调用的过程中，驱动程序管理器将SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC3。 对**SQLAllocHandleStd**的调用等效于对**SQLAllocHandle**的调用，该调用具有SQL_HANDLE_ENV*的句柄类型*，以及对**SQLSetEnvAttr**的调用，以将SQL_ATTR_ODBC_VERSION设置为SQL_OV_ODBC3。  
  
-   如果符合标准的应用程序调用**SQLBindParam（** 这可能是因为**SQLBindParam**是开放组和 ISO CLI 中的有效函数），则 ODBC *3.x*驱动程序管理器将调用映射到**SQLBind参数**中的等效调用。 （请参阅附录 G 中的[SQLBindParam 映射](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)：向后兼容性的驱动程序指南。  
  
-   要与 ISO CLI 保持一致，ODBC *3.x*标头文件包含调用**SQLGetInfo**中使用的信息类型的别名。 符合标准的应用程序可以使用这些别名而不是 ODBC *3.x*信息类型。 有关详细信息，请参阅下一个主题["标题文件](../../../odbc/reference/develop-app/header-files.md)"。  
  
-   符合标准的应用程序必须验证它支持的所有功能是否在其要使用的驱动程序中支持。 将SQL_ATTR_CURSOR_SCROLLABLE语句属性设置为SQL_SCROLLABLE并将SQL_ATTR_CURSOR_SENSITIVITY语句属性设置为SQL_INSENSITIVE或SQL_SENSITIVE是标准中可选功能，但不包括在 ODBC *3.x* Core 级别，因此可能不受所有 ODBC *3.x*驱动程序支持的功能。 如果符合标准的应用程序使用这些功能，它应验证驱动程序是否将使用它们。
