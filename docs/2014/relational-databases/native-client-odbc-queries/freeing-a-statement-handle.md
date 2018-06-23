---
title: 释放语句句柄 |Microsoft 文档
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
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7da2fec15303e9c2d50fb7aa2e6dc40266a380d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124548"
---
# <a name="freeing-a-statement-handle"></a>释放语句句柄
  重用语句句柄比删除它们后再分配新句柄更高效。 对语句句柄执行新 SQL 语句之前，应用程序应当验证当前语句设置是否正确。 这些设置包括语句属性、参数绑定和结果集绑定。 通常情况下，参数和结果设置为旧的 SQL 语句必须通过调用未绑定[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) SQL_RESET_PARAMS 与 SQL_UNBIND 选项，然后重新绑定对于新的 SQL 语句。  
  
 当使用语句完成后应用程序时，它将调用[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)以释放该语句。 请注意， **SQLDisconnect**自动释放连接上的所有语句。  
  
## <a name="see-also"></a>请参阅  
 [执行查询&#40;ODBC&#41;](executing-queries-odbc.md)  
  
  