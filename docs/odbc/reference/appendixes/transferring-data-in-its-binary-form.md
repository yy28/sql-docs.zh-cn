---
description: 以二进制格式传输数据
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
ms.openlocfilehash: ec858729e76c1e360ec0933eca3a29ab17542f4f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386323"
---
# <a name="transferring-data-in-its-binary-form"></a>以二进制格式传输数据
应用程序可以安全地在使用相同 DBMS 和硬件平台的两个数据源之间以指定 DBMS) 使用的内部形式传输数据 (。 对于给定的数据段，源数据源和目标数据源中的 SQL 数据类型必须相同。 C 数据类型为 SQL_C_BINARY。  
  
 当应用程序调用 **SQLFetch**、 **SQLFetchScroll**或 **SQLGetData** 检索源数据源中的数据时，驱动程序将从数据源中检索数据，并将其传输（无需转换）到类型 SQL_C_BINARY 的存储位置。 当应用程序调用 **SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPutData 或 SQLSetPos** 将数据发送到目标数据源时，驱动程序将从存储位置中检索数据，并将其传输到目标数据源而不进行转换。  
  
> [!NOTE]  
>  以这种方式传输除 binary) 数据以外的任何数据 (的应用程序在 Dbms 之间不可互操作。  
  
 **SQLCopyDesc** 可用于将行绑定从源 dbms 复制到目标 dbms 中的参数绑定。
