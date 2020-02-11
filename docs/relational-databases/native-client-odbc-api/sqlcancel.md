---
title: SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 80b0ac3e21933c378d67b41f1bbc846f04811ed5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787655"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)主题指出，在 ODBC 2.x 中，如果应用程序在对语句进行处理时调用**SQLCancel** ，则**SQLCancel**与带有**SQL_CLOSE**选项的**SQLFreeStmt**具有相同的效果;此行为仅用于完整性定义，应用程序应调用**SQLFreeStmt**或**SQLCloseCursor**以关闭游标。 但即使您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 Native Client 应用程序将 odbc API 版本设置为 3.5. x 或更高版本， **SQLCancel**函数也将使用 odbc 2.x 的行为。  
  
## <a name="see-also"></a>另请参阅  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
