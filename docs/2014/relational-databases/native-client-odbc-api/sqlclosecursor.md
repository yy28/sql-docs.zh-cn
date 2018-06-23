---
title: SQLCloseCursor |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b78467ae9648639051480f16eb073a9c48ccb645
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138427"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor**替换[SQLFreeStmt](sqlfreestmt.md)与*选项*SQL_CLOSE 的值。 在收到**SQLCloseCursor**、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将丢弃挂起的结果集行。 请注意，语句的列和参数绑定 （如果存在） 也会保留不变的**SQLCloseCursor**。  
  
## <a name="see-also"></a>请参阅  
 [SQLCloseCursor](http://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  