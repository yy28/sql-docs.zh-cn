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
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360629"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor**取代[SQLFreeStmt](sqlfreestmt.md)与*选项*值 SQL_CLOSE。 在收到**SQLCloseCursor**，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将放弃待定结果集行。 请注意，该语句的列和参数绑定 （如果存在） 也会保留并未改变**SQLCloseCursor**。  
  
## <a name="see-also"></a>请参阅  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
