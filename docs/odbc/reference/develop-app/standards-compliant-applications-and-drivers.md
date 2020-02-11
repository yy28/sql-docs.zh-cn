---
title: 符合标准的应用程序和驱动程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4980cfe64a5a8e8404c6b5b0bdc8b1aba484f0c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107334"
---
# <a name="standards-compliant-applications-and-drivers"></a>符合标准的应用程序和驱动程序
符合标准的应用程序或驱动程序符合开放组 CAE 规范 "数据管理： SQL 调用级别接口（CLI）" 和 ISO/IEC 9075-3:1995 （E）调用级别接口（SQL/CLI）。  
  
 ODBC *2.x*保证以下功能：  
  
-   当*使用 odbc 1.x 标头*文件编译和*链接 odbc 1.x 库，* 以及通过 Odbc *1.x 驱动程序*管理器获得对驱动程序的访问权限时，写入到开放组和 ISO CLI 规范的应用程序将*使用 odbc 1.x 驱动程序或*符合标准的驱动程序。  
  
-   当使用 odbc 1.x 标头文件编译和*链接 odbc 1.x*库时，以及当应用程序*通过 odbc 1.X* *驱动程序*管理器获得对驱动程序的访问权限时，写入到开放组和 ISO CLI 规范的驱动程序将*使用 odbc 1.x*应用程序或符合标准的应用程序。  
  
 符合标准的应用程序和驱动程序用 ODBC_STD 编译标志进行编译。  
  
 符合标准的应用程序会表现出以下行为：  
  
-   如果符合标准的应用程序调用**SQLAllocEnv** （之所以会出现这种情况，是因为**SQLAllocEnv**是开放组和 ISO CLI 中的有效函数），则调用将在编译时映射到**SQLAllocHandleStd** 。 因此，应用程序会在运行时调用**SQLAllocHandleStd**。 在处理此调用的过程中，驱动程序管理器会将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3。 对**SQLAllocHandleStd**的调用等效于对使用*HandleType* SQL_HANDLE_ENV 的**SQLAllocHandle**的调用，并调用**SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 设置为 SQL_OV_ODBC3。  
  
-   如果符合标准的应用程序调用**SQLBindParam** （因为**SQLBindParam**是开放组和 ISO CLI 中的有效函数，则可能会出现这种情况），*则 ODBC 2.x*驱动程序管理器会将调用映射到**SQLBindParameter**中的等效调用。 （有关向后兼容性，请参阅附录 G：驱动程序准则中的[SQLBindParam 映射](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)。）  
  
-   为了与 ISO CLI 保持一致 *，ODBC 3.x*头文件包含对**SQLGetInfo**的调用中使用的信息类型的别名。 符合标准的应用程序可以使用这些别名，而不是*ODBC 2.x*信息类型。 有关详细信息，请参阅下一主题[标头文件](../../../odbc/reference/develop-app/header-files.md)。  
  
-   符合标准的应用程序必须验证它所支持的所有功能是否在将使用的驱动程序中受支持。 将 SQL_ATTR_CURSOR_SCROLLABLE 语句特性设置为 SQL_SCROLLABLE 并将 SQL_ATTR_CURSOR_SENSITIVITY 语句特性设置为 SQL_INSENSITIVE 或 SQL_SENSITIVE 是作为标准中的可选功能提供的功能，但这些功能并不包含在 ODBC 2.x Core 级别中，因此可能不受*所有 odbc 1.x*驱动*程序*支持。 如果符合标准的应用程序使用这些功能，则应该验证它将用于的驱动程序是否支持它们。
