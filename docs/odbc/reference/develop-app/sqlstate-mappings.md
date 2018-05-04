---
title: SQLSTATE 映射 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e3f1dc1e8f0e8cf67ac97c33a7ab6b7137cdd7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlstate-mappings"></a>SQLSTATE 映射
本主题讨论为 ODBC 2 的 SQLSTATE 值。*x*和 ODBC 3。*x*。 有关 ODBC 3 的详细信息。*x* SQLSTATE 值，请参阅[附录 a: ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。  
  
 在 ODBC 3。*x*、 HYxxx SQLSTATEs 返回而不是 S1xxx，以及 42Sxx SQLSTATEs 返回而不是 S00XX。 这样做是为了与 Open Group 和 ISO 标准保持一致。 在许多情况下，映射不一对一因为标准具有重新定义几个 SQLSTATEs 的解释。  
  
 当一个 ODBC 2。*x*应用程序升级到 ODBC 3。*x*应用程序，则应用程序必须将更改为预期 ODBC 3。*x*而不是 ODBC 2 SQLSTATEs。*x* SQLSTATEs。 下表列出了 ODBC 3。*x* SQLSTATEs，每个 ODBC 2。*x* SQLSTATE 映射到。  
  
 当 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC2 时，驱动程序将发送 ODBC 2。*x*而不是 ODBC 3 SQLSTATEs。*x* SQLSTATEs 时**SQLGetDiagField**或**SQLGetDiagRec**调用。 可以注意 ODBC 2 来确定特定映射 *.x*下表，它对应于 ODBC 3 1 列中的 SQLSTATE。*x*第二列中的 SQLSTATE。  
  
|ODBC 2。*x* SQLSTATE|ODBC 3。*x* SQLSTATE|注释|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42S01||  
|S0002|42S02||  
|S0011|42S11||  
|S0012|42S12||  
|S0021|42S21||  
|S0022|42S22||  
|S0023|42S23||  
|S1000|HY000||  
|S1001|HY001||  
|S1002|07009|ODBC 2。*x* SQLSTATE S1002 映射到 ODBC 3。*x* SQLSTATE 07009 如果基础函数**SQLBindCol**， **SQLColAttribute**， **SQLExtendedFetch**， **SQLFetch**， **SQLFetchScroll**，或**SQLGetData**。|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|返回为 null 指针的使用无效。|  
|S1009|HY024|返回为无效的属性值。|  
|S1009|HY092|通过调用返回的更新或删除数据**SQLSetPos**，或添加、 更新或删除数据，通过调用**SQLBulkOperations**，当并发是只读的。|  
|S1010|HY007 HY010|SQLSTATE S1010 映射到 SQLSTATE HY007 时**SQLDescribeCol**在调用之前调用**SQLPrepare**， **SQLExecDirect**，或目录函数*StatementHandle*。 否则，SQLSTATE S1010 映射到 SQLSTATE HY010。|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC 3。*x* SQLSTATE 07009 映射到 ODBC 2。*x* SQLSTATE S1093 如果基础函数**SQLBindParameter**或**SQLDescribeParam**。|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC 3。*x* SQLSTATE 07008 映射到 ODBC 2。*x* SQLSTATE S1000。
