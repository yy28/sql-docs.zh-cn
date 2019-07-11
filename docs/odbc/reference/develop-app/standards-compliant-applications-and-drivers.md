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
manager: craigg
ms.openlocfilehash: 1283cd0b41eff971a1014b213bda5e44f1912039
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792782"
---
# <a name="standards-compliant-applications-and-drivers"></a>符合标准的应用程序和驱动程序
符合标准的应用程序或驱动程序是一个符合开放组 CAE 规范的"数据管理：SQL 调用级别接口 (CLI)"和 ISO/IEC 9075-3:1995 (E) 调用级别接口 (SQL/CLI)。  
  
 ODBC *3.x*保证了以下功能：  
  
-   Open Group 和 ISO CLI 规范编写的应用程序将使用 ODBC *3.x*驱动程序或符合标准的驱动程序时使用 ODBC 编译*3.x*标头文件，并与链接ODBC *3.x*库，并当它获得通过 ODBC 驱动程序的访问权限*3.x*驱动程序管理器。  
  
-   编写 Open Group 和 ISO CLI 规范的驱动程序将使用 ODBC *3.x*应用程序或符合标准的应用程序时使用 ODBC 编译*3.x*标头文件和链接使用 ODBC *3.x*库，并当应用程序获得通过 ODBC 驱动程序的访问权限*3.x*驱动程序管理器。  
  
 使用 ODBC_STD 编译标志编译符合标准的应用程序和驱动程序。  
  
 符合标准的应用程序会显示以下行为：  
  
-   如果符合标准的应用程序调用**SQLAllocEnv** (可能因为**SQLAllocEnv**是 Open Group 和 ISO CLI 中的有效函数)，在调用映射到**SQLAllocHandleStd**在编译时。 因此，在运行时，应用程序调用**SQLAllocHandleStd**。 在处理此调用期间，驱动程序管理器设置为 SQL_OV_ODBC3 SQL_ATTR_ODBC_VERSION 环境属性。 调用**SQLAllocHandleStd**等效于调用**SQLAllocHandle**与*HandleType* SQL_HANDLE_ENV 和调用**SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 设置为 SQL_OV_ODBC3。  
  
-   如果符合标准的应用程序调用**SQLBindParam** (可能因为**SQLBindParam**是 Open Group 和 ISO CLI 中的有效函数)，ODBC *3.x*驱动程序管理器映射中的等效调用在调用**SQLBindParameter**。 (请参阅[SQLBindParam 映射](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)附录 g:驱动程序指南的向后兼容性。）  
  
-   若要符合 ISO CLI，ODBC *3.x*标头文件包含用于调用的信息类型的别名**SQLGetInfo**。 符合标准的应用程序可以使用这些别名而不是 ODBC *3.x*信息类型。 有关详细信息，请参阅下一主题[标头文件](../../../odbc/reference/develop-app/header-files.md)。  
  
-   符合标准的应用程序必须验证，它将使用的驱动程序中支持它支持所有功能。 将 SQL_ATTR_CURSOR_SCROLLABLE 语句属性设置为 SQL_SCROLLABLE 和设置为 SQL_INSENSITIVE 或 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY 语句属性是作为可选功能的标准中可用的功能但不是包括在 ODBC *3.x*核心级别，因此可能不支持所有 ODBC *3.x*驱动程序。 如果符合标准的应用程序使用这些功能，它应验证它会使用该驱动程序支持它们。
