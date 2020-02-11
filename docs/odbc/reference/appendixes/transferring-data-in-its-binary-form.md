---
title: 以二进制格式传输数据 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070017"
---
# <a name="transferring-data-in-its-binary-form"></a>以二进制格式传输数据
应用程序可以安全地在使用相同 DBMS 和硬件平台的两个数据源之间传输数据（由指定 DBMS 使用的内部窗体）。 对于给定的数据段，源数据源和目标数据源中的 SQL 数据类型必须相同。 C 数据类型为 SQL_C_BINARY。  
  
 当应用程序调用**SQLFetch**、 **SQLFetchScroll**或**SQLGetData**检索源数据源中的数据时，驱动程序将从数据源中检索数据，并将其传输（无需转换）到类型 SQL_C_BINARY 的存储位置。 当应用程序调用**SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPutData 或 SQLSetPos**将数据发送到目标数据源时，驱动程序将从存储位置中检索数据，并将其传输到目标数据源而不进行转换。  
  
> [!NOTE]  
>  以这种方式传输任何数据（二进制数据除外）的应用程序在 Dbms 之间不可互操作。  
  
 **SQLCopyDesc**可用于将行绑定从源 dbms 复制到目标 dbms 中的参数绑定。
