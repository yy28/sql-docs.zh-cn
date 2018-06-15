---
title: SQLSetConnectOption （Excel 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Excel Driver
- Excel driver [ODBC], SQLSetConnectOption
ms.assetid: 528d21d1-4516-4497-9da4-7b87d77e622a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47f212a362715d43f522cd4e36bced9ce18825d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904632"
---
# <a name="sqlsetconnectoption-excel-driver"></a>SQLSetConnectOption （Excel 驱动程序）
> [!NOTE]  
>  本主题提供 Excel 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|fOption|注释|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以设置为 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 但是，该驱动程序不会阻止更新，如果 SQL_ACCESS_MODE 设置为 SQL_MODE_READ_ONLY。|  
|SQL_AUTOCOMMIT|Microsoft Excel 驱动程序仅支持 SQL_AUTOCOMMIT 被设置为于 （默认状态），因为它们不支持事务。|  
|SQL_CURRENT_QUALIFIER|支持。|  
|SQL_LOGIN_TIMEOUT|不提供支持。|  
|SQL_OPT_TRACE|支持。|  
|SQL_OPT_TRACEFILE|支持。|  
|SQL_PACKET_SIZE|不提供支持。|  
|SQL_QUIET_MODE|不提供支持。|  
|SQL_TRANSLATE_DLL|不提供支持。|  
|SQL_TRANSLATION_OPTION|不提供支持。|  
|SQL_TXN_ISOLATION|不提供支持。|
