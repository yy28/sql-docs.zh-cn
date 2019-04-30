---
title: SQLSetConnectOption （Access 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18950d49afdab8517b95c59df8841c33b5d3d086
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305634"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|fOption|注释|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以设置为 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 但是，该驱动程序不会阻止更新，如果 SQL_ACCESS_MODE 设置为 SQL_MODE_READ_ONLY。|  
|SQL_AUTOCOMMIT|使用 Microsoft Access 驱动程序时，SQL_AUTOCOMMIT 选项可能设置为 sql_autocommit_on，否则或 SQL_AUTOCOMMIT_OFF，因为 Microsoft Access 驱动程序支持事务 [1]。|  
|SQL_CURRENT_QUALIFIER|支持。|  
|SQL_LOGIN_TIMEOUT|不提供支持。|  
|SQL_OPT_TRACE|支持。|  
|SQL_OPT_TRACEFILE|支持。|  
|SQL_PACKET_SIZE|不提供支持。|  
|SQL_QUIET_MODE|不提供支持。|  
|SQL_TRANSLATE_DLL|不提供支持。|  
|SQL_TRANSLATION_OPTION|不提供支持。|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION 始终是 SQL_TXN_READ_COMMITTED。|  
  
 [1] 原子事务不受 Microsoft Access 驱动程序。 有限延迟时提交事务使用 Microsoft Access 驱动程序，则在提交事务的时间和写入值的时间之间存在到磁盘。 这种延迟取决于 Microsoft Jet 引擎中固有的延迟。 页超时不会小于最小值，即使 PageTimeout 选项设置为低于该值。 因此，没有提交数据不能保证是稳定的因为可能会在延迟期间进行更改。
