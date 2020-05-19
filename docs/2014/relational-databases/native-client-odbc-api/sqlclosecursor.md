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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3e076c7e81a1ccf61813bf5dc629fb3ce59f5070
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706361"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor**使用*选项*值 SQL_CLOSE 来替换[SQLFreeStmt](sqlfreestmt.md) 。 收到**SQLCloseCursor**后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将放弃挂起的结果集行。 请注意， **SQLCloseCursor**不会改变语句的列和参数绑定（如果存在）。  
  
## <a name="see-also"></a>另请参阅  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
