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
ms.openlocfilehash: bea124a78e2a180180c59de3577fe1db7637e110
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67897787"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|fOption|注释|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以设置为 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 但是，如果 SQL_ACCESS_MODE 设置为 SQL_MODE_READ_ONLY，驱动程序不会阻止更新。|  
|SQL_AUTOCOMMIT|使用 Microsoft Access 驱动程序时，可以将 SQL_AUTOCOMMIT 选项设置为 SQL_AUTOCOMMIT_ON 或 SQL_AUTOCOMMIT_OFF，因为 Microsoft Access 驱动程序支持事务 [1]。|  
|SQL_CURRENT_QUALIFIER|。|  
|SQL_LOGIN_TIMEOUT|不支持。|  
|SQL_OPT_TRACE|。|  
|SQL_OPT_TRACEFILE|。|  
|SQL_PACKET_SIZE|不支持。|  
|SQL_QUIET_MODE|不支持。|  
|SQL_TRANSLATE_DLL|不支持。|  
|SQL_TRANSLATION_OPTION|不支持。|  
|SQL_TXN_ISOLATION|始终 SQL_TXN_READ_COMMITTED SQL_TXN_ISOLATION。|  
  
 [1] Microsoft Access 驱动程序不支持原子事务。 使用 Microsoft Access 驱动程序提交事务时，提交事务的时间与将值写入磁盘之间存在一定的延迟。 此延迟取决于 Microsoft Jet 引擎固有的延迟。 即使将 PageTimeout 选项设置为低于该值，页面超时也不会小于最小值。 因此，无法保证提交的数据是稳定的，因为可能会在延迟期间做出更改。
