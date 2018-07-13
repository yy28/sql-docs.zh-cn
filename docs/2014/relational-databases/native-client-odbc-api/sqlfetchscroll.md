---
title: SQLFetchScroll |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fa4b974c834581158c6bf60e4abecfb51b9e8c7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410036"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
  **SQLFetchScroll**返回应用程序的数据的一个行集。 使用设置行集的大小[SQLSetStmtAttr](sqlsetstmtattr.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持所有定义的提取指令 （例如，sql_fetch_relative），但有以下限制：  
  
-   如果为语句定义了只进游标，则必须使用 SQL_FETCH_NEXT，尝试以任何其他方式执行提取都将导致返回错误。  
  
-   仅静态和键集驱动游标支持 SQL_FETCH_BOOKMARK。  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>SQLFetchScroll 对日期和时间增强功能的支持  
 结果列的日期/时间类型的值将转换中所述[从 SQL 到 C 转换](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>SQLFetchScroll 对大型 CLR UDT 的支持  
 **SQLFetchScroll**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLFetchScroll 函数](http://go.microsoft.com/fwlink/?LinkId=59343)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
