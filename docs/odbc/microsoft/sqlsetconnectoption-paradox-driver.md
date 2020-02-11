---
title: SQLSetConnectOption （Paradox 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLSetConnectOption
ms.assetid: 050ee2be-594e-4dbd-af67-8b6aae756cd1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cf6d01650b86fca4c782521fe3c368f729e6b42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67897763"
---
# <a name="sqlsetconnectoption-paradox-driver"></a>SQLSetConnectOption（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供了特定于驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|fOption|注释|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以设置为 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 但是，如果 SQL_ACCESS_MODE 设置为 SQL_MODE_READ_ONLY，驱动程序不会阻止更新。|  
|SQL_AUTOCOMMIT|Paradox 驱动程序只支持将 SQL_AUTOCOMMIT 设置为 ON （默认状态），因为它们不支持事务。|  
|SQL_CURRENT_QUALIFIER|。|  
|SQL_LOGIN_TIMEOUT|不支持。|  
|SQL_OPT_TRACE|。|  
|SQL_OPT_TRACEFILE|。|  
|SQL_PACKET_SIZE|不支持。|  
|SQL_QUIET_MODE|不支持。|  
|SQL_TRANSLATE_DLL|不支持。|  
|SQL_TRANSLATION_OPTION|不支持。|  
|SQL_TXN_ISOLATION|不支持。|
