---
title: SQLSetEnvAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b53db46db783bd55799c251d38d86d4479e7ee0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844405"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [ODBC 程序员参考](http://go.microsoft.com/fwlink/?LinkId=45250)定义的 ODBC 驱动程序应如何解释**SQLSetEnvAttr**属性来自于 ODBC 2 编写的应用程序的规范。*x*或 ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序符合这些规则。  
  
 由控制的属性之一**SQLSetEnvAttr**是是否连接池是要使用。 如果连接池用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序*DriverCompletion*时使用连接参数必须设置为 SQL_DRIVER_NOPROMPT [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)或**SQLConnect**。  
  
## <a name="see-also"></a>请参阅  
 [SQLSetEnvAttr 函数](http://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
