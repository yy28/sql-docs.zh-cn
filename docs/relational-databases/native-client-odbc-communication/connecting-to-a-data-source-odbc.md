---
title: 连接到数据源 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- checking connection states
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- SQLBrowseConnect function
- ODBC applications, connections
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLConnect function
- SQLDriveConnect function
- verifying connection states
- SQL Server Native Client ODBC driver, data sources
- SQL Server Native Client ODBC driver, connections
ms.assetid: ae30dd1d-06ae-452b-9618-8fd8cd7ba074
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cab7a4d1bf17fc1e58b8f778b862d47f19b898e9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43076279"
---
# <a name="connecting-to-a-data-source-odbc"></a>连接数据源 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在分配环境和连接句柄并设置连接属性后，应用程序将连接到数据源或驱动程序。 有三种可用于连接的函数：  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 有关建立连接到数据源，包括可用的各种连接字符串选项的详细信息请参阅[将连接字符串关键字用于 SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect**是最简单的连接函数。 它接受三个参数：数据源名称、用户 ID 和密码。 使用**SQLConnect**当这三个参数包含连接到数据库所需的所有信息。 若要执行此操作，生成的数据源使用列表**SQLDataSources**; 提示用户输入数据源、 用户 ID 和密码;，然后调用**SQLConnect**。  
  
 **SQLConnect**假定数据源名称、 用户 ID 和密码都不足以连接到数据源和 ODBC 数据源包含 ODBC 驱动程序建立连接所需的所有其他信息。 与不同[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)并[SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)， **SQLConnect**不使用连接字符串。  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect**需要比数据源名称、 用户 ID 和密码的详细信息时使用。 参数之一**SQLDriverConnect**是一个包含特定于驱动程序的信息的连接字符串。 可以使用**SQLDriverConnect**而不是**SQLConnect**原因如下：  
  
-   在连接时指定特定于驱动程序的信息。  
  
-   请求驱动程序提示用户输入连接信息。  
  
-   不使用 ODBC 数据源进行连接。  
  
 **SQLDriverConnect**连接字符串包含一系列指定 ODBC 驱动程序支持的所有连接信息的关键字值对。 每个驱动程序都支持标准 ODBC 关键字（DSN、FILEDSN、DRIVER、UID、PWD 和 SAVEFILE），以及用于驱动程序支持的所有连接信息的特定于驱动程序的关键字。 **SQLDriverConnect**可用于不使用数据源连接。 例如，应用程序专为"无 DSN"连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以调用**SQLDriverConnect**定义登录 ID、 密码、 网络库、 服务器名称的连接字符串连接和默认数据库使用。  
  
 使用时**SQLDriverConnect**，有两个选项可用于提示用户输入所需的连接信息：  
  
-   应用程序对话框  
  
     可以创建一个应用程序对话框，提示输入连接信息，然后调用**SQLDriverConnect**提供了 NULL 窗口句柄并*DriverCompletion*设置为 SQL_DRIVER_NOPROMPT。 这些参数设置将禁止 ODBC 驱动程序打开自己的对话框。 在对应用程序的用户界面进行控制非常重要时，使用此方法。  
  
-   驱动程序对话框  
  
     您可以编写代码传递有效的窗口句柄的应用程序**SQLDriverConnect**并设置*DriverCompletion*为 SQL_DRIVER_COMPLETE、 SQL_DRIVER_PROMPT 或 SQL_DRIVER_COMPLETE_ 参数必填。 驱动程序然后生成一个对话框，以便提示用户输入连接信息。 此方法可以简化应用程序代码。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**，例如**SQLDriverConnect**，使用连接字符串。 但是，通过使用**SQLBrowseConnect**，应用程序可以在运行时构造完整连接字符串以迭代方式与数据源。 这允许应用程序执行以下两种操作：  
  
-   生成自己的对话框以提示输入此信息，因此保留对其用户界面的控制。  
  
-   浏览系统以找到可由特定的驱动程序使用的数据源，这可能要执行若干步骤。  
  
     例如，用户可能要首先浏览网络以找到服务器，然后在选择某一服务器后，浏览该服务器以找到驱动程序可访问的数据库。  
  
 当**SQLBrowseConnect**完成成功连接后，它返回可在后续调用使用的连接字符串**SQLDriverConnect**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序始终对成功返回 SQL_SUCCESS_WITH_INFO **SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**。 当 ODBC 应用程序调用**SQLGetDiagRec**后获取 SQL_SUCCESS_WITH_INFO，它可以接收下列消息：  
  
 5701  
 指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将用户的上下文置于在数据源中定义的默认数据库中，或者置于为在连接中使用的登录 ID 定义的默认数据库中（如果数据源没有默认数据库）。  
  
 5703  
 指示要在服务器上使用的语言。  
  
 以下示例显示系统管理员对成功的连接返回的消息：  
  
```  
szSqlState = "01000", *pfNativeError = 5701,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed database context to 'pubs'."  
szSqlState = "01000", *pfNativeError = 5703,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed language setting to 'us_english'."  
```  
  
 您可以忽略消息 5701 和 5703；它们仅供参考。 但是，不应忽视 SQL_SUCCESS_WITH_INFO 返回代码，因为可能返回并非 5701 或 5703 的其他消息。 例如，如果驱动程序连接到运行的实例的服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]过时的目录存储过程的一个错误返回通过**SQLGetDiagRec** SQL_SUCCESS_WITH_INFO 后：  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 错误处理的应用程序的函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接应调用**SQLGetDiagRec**直到它返回 sql_no_data 为止。 它然后应作用于与以外的任何消息*pfNative* 5701 或 5703 的代码。  
  
## <a name="see-also"></a>请参阅  
 [与 SQL Server 通信&#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
