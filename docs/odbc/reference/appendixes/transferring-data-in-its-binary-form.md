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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53531ff4a3b2e1441fabf22ec7a3ce12b15540eb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301409"
---
# <a name="transferring-data-in-its-binary-form"></a>以二进制格式传输数据
应用程序可以安全地在使用相同 DBMS 和硬件平台的两个数据源之间传输数据（由指定 DBMS 使用的内部窗体）。 对于给定的数据段，源数据源和目标数据源中的 SQL 数据类型必须相同。 C 数据类型为 SQL_C_BINARY。  
  
 当应用程序调用**SQLFetch**、 **SQLFetchScroll**或**SQLGetData**检索源数据源中的数据时，驱动程序将从数据源中检索数据，并将其传输（无需转换）到类型 SQL_C_BINARY 的存储位置。 当应用程序调用**SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPutData 或 SQLSetPos**将数据发送到目标数据源时，驱动程序将从存储位置中检索数据，并将其传输到目标数据源而不进行转换。  
  
> [!NOTE]  
>  以这种方式传输任何数据（二进制数据除外）的应用程序在 Dbms 之间不可互操作。  
  
 **SQLCopyDesc**可用于将行绑定从源 dbms 复制到目标 dbms 中的参数绑定。
