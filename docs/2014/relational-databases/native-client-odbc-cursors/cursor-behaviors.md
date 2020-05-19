---
title: 游标行为 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7d6b41e72d3421d24a160dbcc226ce285e37981c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702046"
---
# <a name="cursor-behaviors"></a>游标行为
  ODBC 支持通过指定游标的可滚动性和敏感性来指定其行为的 ISO 选项。 这些行为是通过在对[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)的调用上设置 SQL_ATTR_CURSOR_SCROLLABLE 和 SQL_ATTR_CURSOR_SENSITIVITY 选项来指定的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通过请求具有以下特征的服务器游标来实现这些选项。  
  
|游标行为设置|请求的服务器游标的特征|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 和 SQL_SENSITIVE|由键集驱动的游标和基于版本的乐观并发|  
|SQL_SCROLLABLE 和 SQL_INSENSITIVE|静态游标和只读并发|  
|SQL_SCROLLABLE 和 SQL_UNSPECIFIED|静态游标和只读并发|  
|SQL_NONSCROLLABLE 和 SQL_SENSITIVE|只进游标和基于版本的乐观并发|  
|SQL_NONSCROLLABLE 和 SQL_INSENSITIVE|默认结果集（只进，只读）|  
|SQL_NONSCROLLABLE 和 SQL_UNSPECIFIED|默认结果集（只进，只读）|  
  
 基于版本的乐观并发要求基础表中有一个**时间戳**列。 如果对没有**时间戳**列的表请求基于版本的乐观并发控制，则服务器将使用基于值的乐观并发。  
  
## <a name="scrollability"></a>可滚动性  
 当 SQL_ATTR_CURSOR_SCROLLABLE 设置为 SQL_SCROLLABLE 时，游标支持[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)的*FetchOrientation*参数的所有不同值。 当 SQL_ATTR_CURSOR_SCROLLABLE 设置为 SQL_NONSCROLLABLE 时，游标仅支持 SQL_FETCH_NEXT 的*FetchOrientation*值。  
  
## <a name="sensitivity"></a>敏感性  
 将 SQL_ATTR_CURSOR_SENSITIVITY 设置为 SQL_SENSITIVE 时，游标可以反映由当前用户所做的或由其他用户提交的数据修改。 将 SQL_ATTR_CURSOR_SENSITIVITY 设置为 SQL_INSENSITIVE 时，游标不能反映数据修改。  
  
## <a name="see-also"></a>另请参阅  
 [使用游标 &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
