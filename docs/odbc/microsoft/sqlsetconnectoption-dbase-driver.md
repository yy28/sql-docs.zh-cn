---
title: SQLSetConnectOption (dBASE 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], dBASE Driver
ms.assetid: b1924c33-6820-4566-b716-6897807edd0f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0b3c421ad00a1627ddfb7e6f4fb63ee5d30981a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618785"
---
# <a name="sqlsetconnectoption-dbase-driver"></a>SQLSetConnectOption（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供 dBASE 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|fOption|注释|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以设置为 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 但是，该驱动程序不会阻止更新，如果 SQL_ACCESS_MODE 设置为 SQL_MODE_READ_ONLY。|  
|SQL_AUTOCOMMIT|DBASE 驱动程序仅支持 SQL_AUTOCOMMIT 上 （默认状态），设置为，因为它不支持事务。|  
|SQL_CURRENT_QUALIFIER|支持。|  
|SQL_LOGIN_TIMEOUT|不提供支持。|  
|SQL_OPT_TRACE|支持。|  
|SQL_OPT_TRACEFILE|支持。|  
|SQL_PACKET_SIZE|不提供支持。|  
|SQL_QUIET_MODE|不提供支持。|  
|SQL_TRANSLATE_DLL|不提供支持。|  
|SQL_TRANSLATION_OPTION|不提供支持。|  
|SQL_TXN_ISOLATION|不提供支持。|
