---
title: 将以其二进制形式的数据传输 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2d1227af9eeb303bc0d9bc56733e6bda9b5325c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="transferring-data-in-its-binary-form"></a>以二进制格式传输数据
应用程序可以安全地使用相同的 DBMS 和硬件平台的两个数据源之间传输 （中由指定的 DBMS 的内部形式） 的数据。 给定的一段的数据，SQL 数据类型必须是源和目标数据源中相同。 C 数据类型为 SQL_C_BINARY。  
  
 在应用程序调用**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**若要从源数据源检索数据，该驱动程序检索数据从数据源，并将其，传输不转换，为类型 SQL_C_BINARY 的存储位置。 在应用程序调用**SQLBulkOperations**， **SQLExecute**， **SQLExecDirect**， **SQLPutData 或 SQLSetPos**发送到数据目标数据源，该驱动程序从存储位置检索数据，并将其，传输不转换，为目标数据源。  
  
> [!NOTE]  
>  以这种方式传输 （二进制数据除外） 的任何数据的应用程序不在 Dbms 之间的可互操作。  
  
 **SQLCopyDesc**可以用于将行绑定源 DBMS 中复制到目标 DBMS 中的参数绑定。
