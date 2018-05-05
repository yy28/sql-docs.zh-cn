---
title: 符合标准的应用程序和驱动程序 |Microsoft 文档
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
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc733f6a9bf4d7edeae5c06f577b206f8232281b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="standards-compliant-applications-and-drivers"></a>符合标准的应用程序和驱动程序
符合标准的应用程序或驱动程序是一个符合打开组 CAE 规范"数据管理:: SQL 调用级界面 (CLI)，"和 ISO/IEC 9075-3:1995 (E) 调用级接口 (SQL/CLI)。  
  
 ODBC 3 *.x*保证以下功能：  
  
-   Open Group 和 ISO CLI 规范编写的应用程序会使用 ODBC 3 *.x*驱动程序或符合标准的驱动程序时使用 ODBC 3 编译 *.x*标头文件，并与链接ODBC 3 *.x*库，当它获取对通过 ODBC 3 驱动程序访问权限 *.x*驱动程序管理器。  
  
-   写入到 Open Group 和 ISO CLI 规范的驱动程序会使用 ODBC 3 *.x*应用程序或一个符合标准的应用程序时使用 ODBC 3 编译 *.x*标头文件和链接ODBC 3 *.x*库，并当应用程序获得到通过 ODBC 3 驱动程序的访问权限 *.x*驱动程序管理器。  
  
 使用 ODBC_STD 编译标志编译符合标准的应用程序和驱动程序。  
  
 符合标准的应用程序会显示以下行为：  
  
-   如果符合标准的应用程序调用**SQLAllocEnv** (因为有**SQLAllocEnv**是 Open Group 和 ISO CLI 中的有效函数)，调用映射到**SQLAllocHandleStd**在编译时。 因此，在运行时，在应用程序调用**SQLAllocHandleStd**。 在处理此调用的过程中，驱动程序管理器将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3。 调用**SQLAllocHandleStd**等效于调用**SQLAllocHandle**与*HandleType* SQL_HANDLE_ENV 和调用**SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 设置为 SQL_OV_ODBC3。  
  
-   如果符合标准的应用程序调用**SQLBindParam** (因为有**SQLBindParam**是 Open Group 和 ISO CLI 中的有效函数)，ODBC 3 *.x*驱动程序管理器映射中的等效调用调用**SQLBindParameter**。 (请参阅[SQLBindParam 映射](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)为了向后兼容的附录 g： 驱动程序准则中。)  
  
-   若要符合 ISO CLI，ODBC 3 *.x*标头文件包含对调用中使用的信息类型的别名**SQLGetInfo**。 符合标准的应用程序可以使用这些别名，而不是 ODBC 3 *.x*信息类型。 有关详细信息，请参阅下一主题[标头文件](../../../odbc/reference/develop-app/header-files.md)。  
  
-   符合标准的应用程序必须验证它将与兼容的驱动程序支持它支持的所有功能。 将 SQL_ATTR_CURSOR_SCROLLABLE 语句属性设置为 SQL_SCROLLABLE 和设置到 SQL_INSENSITIVE 或 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY 语句属性提供了可用作标准中的可选功能的功能但不是包括在 ODBC 3 *.x*核心级别，因此可能不支持由所有 ODBC 3 *.x*驱动程序。 如果符合标准的应用程序使用这些功能，它应验证它将与兼容的驱动程序支持它们。
