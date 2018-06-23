---
title: 游标行为 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 15aee78cfc531a7b80e034021b26404e5735a0ec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013860"
---
# <a name="cursor-behaviors"></a>游标行为
  ODBC 支持通过指定游标的可滚动性和敏感性来指定其行为的 ISO 选项。 这些行为指定通过在调用设置 SQL_ATTR_CURSOR_SCROLLABLE 和 SQL_ATTR_CURSOR_SENSITIVITY [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通过请求具有以下特征的服务器游标来实现这些选项。  
  
|游标行为设置|请求的服务器游标的特征|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 和 SQL_SENSITIVE|由键集驱动的游标和基于版本的乐观并发|  
|SQL_SCROLLABLE 和 SQL_INSENSITIVE|静态游标和只读并发|  
|SQL_SCROLLABLE 和 SQL_UNSPECIFIED|静态游标和只读并发|  
|SQL_NONSCROLLABLE 和 SQL_SENSITIVE|只进游标和基于版本的乐观并发|  
|SQL_NONSCROLLABLE 和 SQL_INSENSITIVE|默认结果集（只进，只读）|  
|SQL_NONSCROLLABLE 和 SQL_UNSPECIFIED|默认结果集（只进，只读）|  
  
 基于版本的开放式并发需要**时间戳**基础表中的列。 如果没有的表上请求基于版本乐观并发控制**时间戳**列中，服务器使用基于值的开放式并发。  
  
## <a name="scrollability"></a>可滚动性  
 当 SQL_ATTR_CURSOR_SCROLLABLE 设置为 SQL_SCROLLABLE 时，光标支持的所有不同值*FetchOrientation*参数[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)。 当 SQL_ATTR_CURSOR_SCROLLABLE 设置为 SQL_NONSCROLLABLE 时，仅支持光标*FetchOrientation* SQL_FETCH_NEXT 的值。  
  
## <a name="sensitivity"></a>敏感性  
 将 SQL_ATTR_CURSOR_SENSITIVITY 设置为 SQL_SENSITIVE 时，游标可以反映由当前用户所做的或由其他用户提交的数据修改。 将 SQL_ATTR_CURSOR_SENSITIVITY 设置为 SQL_INSENSITIVE 时，游标不能反映数据修改。  
  
## <a name="see-also"></a>请参阅  
 [使用游标， &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  