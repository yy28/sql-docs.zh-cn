---
title: SQLCloseCursor |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da7d6541f7bf31920519cc7462bdfd24a5f6dc0d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067683"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor**使用*选项*值 SQL_CLOSE 来替换[SQLFreeStmt](sqlfreestmt.md) 。 收到**SQLCloseCursor**后，NATIVE Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驱动程序将放弃挂起的结果集行。 请注意， **SQLCloseCursor**不会改变语句的列和参数绑定（如果存在）。  
  
## <a name="see-also"></a>另请参阅  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
