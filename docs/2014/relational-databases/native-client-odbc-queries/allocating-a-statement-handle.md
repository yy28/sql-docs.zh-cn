---
title: 分配的语句句柄 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- statements [ODBC], statement handles
- ODBC applications, executing queries
- SQLGetStmtAttr function
- SQL Server Native Client ODBC driver, statements
- allocating statement handles
- ODBC applications, statements
- statement handles [ODBC]
- SQLAllocHandle function
ms.assetid: 9ee207f3-2667-45f5-87ca-e6efa1fd7a5c
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1609155d816e681eb8469069fc6f7efcd3f06528
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126294"
---
# <a name="allocating-a-statement-handle"></a>分配的语句句柄
  在应用程序可以执行语句之前，它必须分配语句句柄。 这是通过调用**SQLAllocHandle**与*HandleType*参数设置为 SQL_HANDLE_STMT 和*InputHandle*指向连接句柄。  
  
 语句属性是语句句柄的特征。 示例语句属性可以包括使用书签以及用于语句结果集的游标类型。 与设置语句属性[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)，并通过检索它们的当前设置[SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md)。 不要求应用程序设置任何语句属性；所有语句属性都具有默认值，并且某些语句属性是驱动程序特定的。  
  
 使用多个 ODBC 语句和连接选项时，请务必小心。 调用[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)与*fOption*设置为 SQL_ATTR_LOGIN_TIMEOUT 控件正在等待在建立连接 (0 应用程序在尝试连接到超时等待的时间指定无限期等待）。 响应时间较长的站点可以将此值设置为较高的值，以确保具有充足的时间完成连接。 然而，间隔应始终足够短，这样，当驱动程序无法连接时，可以在合理的时间内向用户提供回复。  
  
 调用**SQLSetStmtAttr**与*fOption*设置为 SQL_ATTR_QUERY_TIMEOUT 设置查询超时间隔，以帮助防止查询长时间运行的服务器和用户。  
  
 调用**SQLSetStmtAttr**与*fOption*的量进行限制设置为 SQL_ATTR_MAX_LENGTH**文本**和**映像**数据，可以检索单独的语句。 调用**SQLSetStmtAttr**与*fOption*设置为 SQL_ATTR_MAX_ROWS 还限制到第一个行集*n*行，则所有应用程序需要。 请注意，设置 SQL_ATTR_MAX_ROWS 会导致驱动程序向服务器发出 SET ROWCOUNT 语句。 这会影响所有[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语句，其中包括触发器和更新。  
  
 当您设置这些选项时，请务必小心。 最好是连接句柄中的所有语句句柄对于 SQL_ATTR_MAX_LENGTH 和 SQL_ATTR_MAX_ROWS 都具有相同的设置。 如果驱动程序从一个语句句柄切换到另一个对于这些选项具有不同值的语句句柄，则驱动程序必须生成适当的 SET TEXTSIZE 和 SET ROWCOUNT 语句以更改这些设置。 驱动程序无法将这些语句与用户 SQL 语句放在相同的批中，因为用户 SQL 语句可能包含必须为批中第一条语句的语句。 驱动程序必须在单独的批中发送 SET TEXTSIZE 和 SET ROWCOUNT 语句，这会自动生成到服务器的一次附加往返。  
  
## <a name="see-also"></a>请参阅  
 [执行查询&#40;ODBC&#41;](executing-queries-odbc.md)  
  
  