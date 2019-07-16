---
title: 将以二进制格式的数据传输 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2897f882dc9dcd78ee8b919de01126d6be510c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070017"
---
# <a name="transferring-data-in-its-binary-form"></a>以二进制格式传输数据
应用程序可以安全地使用相同的 DBMS 和硬件平台的两个数据源之间传输数据 （在使用通过指定 DBMS 的内部形式）。 为特定的数据，SQL 数据类型必须是源和目标数据源中相同。 C 数据类型为 SQL_C_BINARY。  
  
 当应用程序调用**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**若要从数据源检索数据，该驱动程序检索数据的数据源，然后传输，而无需转换，为类型 SQL_C_BINARY 的存储位置。 当应用程序调用**SQLBulkOperations**， **SQLExecute**， **SQLExecDirect**， **SQLPutData 或 SQLSetPos**若要向其发送数据目标数据源驱动程序从存储位置检索数据和传输，而无需转换，为目标数据源。  
  
> [!NOTE]  
>  以这种方式传输任何数据 （二进制数据除外） 的应用程序不在 Dbms 之间的互操作性。  
  
 **SQLCopyDesc**可用于将行绑定源 DBMS 中复制到目标 DBMS 中的参数绑定。
