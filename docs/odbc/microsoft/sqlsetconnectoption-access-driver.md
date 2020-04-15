---
title: SQLSetConnectOption（访问驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e5f15575d34031d9886219af5677b4fc5f1d5aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301530"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|fOption|注释|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以设置为SQL_MODE_READ_ONLY或SQL_MODE_READ_WRITE。 但是，如果SQL_ACCESS_MODE设置为SQL_MODE_READ_ONLY，则驱动程序不会阻止更新。|  
|SQL_AUTOCOMMIT|使用 Microsoft Access 驱动程序时，SQL_AUTOCOMMIT 选项可以设置为SQL_AUTOCOMMIT_ON或SQL_AUTOCOMMIT_OFF，因为 Microsoft Access 驱动程序支持事务[1]。|  
|SQL_CURRENT_QUALIFIER|支持。|  
|SQL_LOGIN_TIMEOUT|不支持。|  
|SQL_OPT_TRACE|支持。|  
|SQL_OPT_TRACEFILE|支持。|  
|SQL_PACKET_SIZE|不支持。|  
|SQL_QUIET_MODE|不支持。|  
|SQL_TRANSLATE_DLL|不支持。|  
|SQL_TRANSLATION_OPTION|不支持。|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION总是SQL_TXN_READ_COMMITTED。|  
  
 [1] 微软访问驱动程序不支持原子事务。 使用 Microsoft Access 驱动程序提交事务时，提交事务的时间与将值写入磁盘之间的延迟有限。 此延迟由 Microsoft Jet 引擎固有的延迟决定。 即使"PageTimeout"选项设置为低于该值，页面超时也不会小于最小值。 因此，无法保证提交的数据是稳定的，因为可能在延迟期间进行更改。
