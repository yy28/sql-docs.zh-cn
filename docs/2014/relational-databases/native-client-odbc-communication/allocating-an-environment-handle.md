---
title: 分配环境句柄 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66afa14ccb1953265f526f8c8861237638f569fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63199030"
---
# <a name="allocating-an-environment-handle"></a>分配环境句柄
  在应用程序可以调用任何 ODBC 函数之前，它必须初始化 ODBC 环境并分配环境句柄。 这是全局上下文句柄，并且是 ODBC 中其他句柄的占位符。 为此，可调用**SQLAllocHandle** ，并将*HandleType*参数设置为 SQL_HANDLE_ENV 并将*将 inputhandle*设置为 SQL_NULL_HANDLE。  
  
 分配环境句柄之后，应用程序必须设置环境属性以指示它将使用哪一个版本的 ODBC 函数调用。 使用 ODBC 3。*x*函数调用[SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) ，并将*特性*参数设置为 SQL_ATTR_ODBC_VERSION，将*将 valueptr*设置为 SQL_OV_ODBC3。  
  
## <a name="see-also"></a>另请参阅  
 [与 SQL Server &#40;ODBC&#41;通信](communicating-with-sql-server-odbc.md)  
  
  
