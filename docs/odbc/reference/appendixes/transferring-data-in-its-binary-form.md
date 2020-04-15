---
title: 以二进制形式传输数据 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301409"
---
# <a name="transferring-data-in-its-binary-form"></a>以二进制格式传输数据
应用程序可以在使用同一 DBMS 和硬件平台的两个数据源之间安全地传输数据（以指定的 DBMS 使用的内部形式）。 对于给定的数据段，SQL 数据类型在源和目标数据源中必须相同。 C 数据类型SQL_C_BINARY。  
  
 当应用程序调用**SQLFetch、SQLFetchScroll**或**SQLGetData**从源数据源检索数据时，驱动程序会从数据源检索数据，并将其传输到SQL_C_BINARY类型的存储位置，而无需转换。 **SQLFetchScroll** 当应用程序调用**SQLBulk 操作**、SQLExecute、SQLExecDirect、SQLPutData**或 SQLSetPos**将数据发送到目标数据源时，驱动程序将从存储位置检索数据，并将其传输到目标数据源，而无需转换。 **SQLExecute** **SQLExecDirect**  
  
> [!NOTE]  
>  以这种方式传输任何数据（二进制数据除外）的应用程序在 DBMS 之间不可互操作。  
  
 **SQLCopyDesc**可用于将行绑定从源 DBMS 复制到目标 DBMS 中的参数绑定。
