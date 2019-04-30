---
title: 释放语句句柄 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b1a155f7d2ee6cc5f92d46c2bb744168dc5ebc0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200047"
---
# <a name="freeing-a-statement-handle"></a>释放语句句柄
  重用语句句柄比删除它们后再分配新句柄更高效。 对语句句柄执行新 SQL 语句之前，应用程序应当验证当前语句设置是否正确。 这些设置包括语句属性、参数绑定和结果集绑定。 通常情况下，参数和结果集的旧的 SQL 语句必须通过调用未绑定[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) SQL_RESET_PARAMS 和 SQL_UNBIND 选项，然后重新绑定为新的 SQL 语句。  
  
 当应用程序使用完该语句时，它将调用[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)释放语句。 请注意， **SQLDisconnect**自动释放连接上的所有语句。  
  
## <a name="see-also"></a>请参阅  
 [执行查询&#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
