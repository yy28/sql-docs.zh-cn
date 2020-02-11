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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200047"
---
# <a name="freeing-a-statement-handle"></a>释放语句句柄
  重用语句句柄比删除它们后再分配新句柄更高效。 对语句句柄执行新 SQL 语句之前，应用程序应当验证当前语句设置是否正确。 这些设置包括语句属性、参数绑定和结果集绑定。 通常，旧 SQL 语句的参数和结果集必须通过使用 SQL_RESET_PARAMS 和 SQL_UNBIND 选项调用[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md)进行取消绑定，然后再为新的 sql 语句重新绑定。  
  
 当应用程序使用完该语句后，它将调用[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)来释放该语句。 请注意， **SQLDisconnect**会自动释放连接上的所有语句。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;执行查询](executing-queries-odbc.md)  
  
  
