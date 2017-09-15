---
title: "SQLSetConnectOption （Access 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b8f7497cb6b36602908443ab4fd9bdeb592ce8af
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption （Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|fOption|注释|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以设置为 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 但是，该驱动程序不会阻止更新，如果 SQL_ACCESS_MODE 设置为 SQL_MODE_READ_ONLY。|  
|SQL_AUTOCOMMIT|当使用 Microsoft Access 驱动程序时，SQL_AUTOCOMMIT 选项可能设置为 SQL_AUTOCOMMIT_ON 或 SQL_AUTOCOMMIT_OFF，因为 Microsoft Access 驱动程序支持事务 [1]。|  
|SQL_CURRENT_QUALIFIER|支持。|  
|SQL_LOGIN_TIMEOUT|不提供支持。|  
|SQL_OPT_TRACE|支持。|  
|SQL_OPT_TRACEFILE|支持。|  
|SQL_PACKET_SIZE|不提供支持。|  
|SQL_QUIET_MODE|不提供支持。|  
|SQL_TRANSLATE_DLL|不提供支持。|  
|SQL_TRANSLATION_OPTION|不提供支持。|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION 始终是 SQL_TXN_READ_COMMITTED。|  
  
 [1] 原子事务不受 Microsoft Access 驱动程序。 有限的延迟时提交事务使用 Microsoft Access 驱动程序，则提交此事务的时间和写入值的时间之间存在到磁盘。 此延迟是由 Microsoft Jet 引擎中的固有延迟确定的。 页超时不将会小于最小值，即使 PageTimeout 选项设置为低于此值。 因此，没有提交数据不能保证是稳定的因为可能会延迟过程中进行更改。
