---
title: SQLSetConnectOption (dBASE 驱动程序) |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], dBASE Driver
ms.assetid: b1924c33-6820-4566-b716-6897807edd0f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 25585d7719eeb615dab2ec3f55c58b240b8e1bbc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetconnectoption-dbase-driver"></a>SQLSetConnectOption (dBASE 驱动程序)
> [!NOTE]  
>  本主题提供 dBASE 特定于驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|fOption|注释|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以设置为 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 但是，该驱动程序不会阻止更新，如果 SQL_ACCESS_MODE 设置为 SQL_MODE_READ_ONLY。|  
|SQL_AUTOCOMMIT|DBASE 驱动程序仅支持 SQL_AUTOCOMMIT 被设置为于 （默认状态），因为它不支持事务。|  
|SQL_CURRENT_QUALIFIER|支持。|  
|SQL_LOGIN_TIMEOUT|不提供支持。|  
|SQL_OPT_TRACE|支持。|  
|SQL_OPT_TRACEFILE|支持。|  
|SQL_PACKET_SIZE|不提供支持。|  
|SQL_QUIET_MODE|不提供支持。|  
|SQL_TRANSLATE_DLL|不提供支持。|  
|SQL_TRANSLATION_OPTION|不提供支持。|  
|SQL_TXN_ISOLATION|不提供支持。|
