---
title: SQLSTATE 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec58c0e41869529bbba5fd31ad534976923a990d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299737"
---
# <a name="sqlstate-mappings"></a>SQLSTATE 映射
本主题讨论 ODBC *2.x 和 odbc* 2.X 的 SQLSTATE*值。* 有关 ODBC *2.X SQLSTATE 值*的详细信息，请参阅[附录 A： ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。  
  
 在 ODBC 3.x 中，会返回 HYxxx SQLSTATEs 而不是*S1xxx，并*返回 42Sxx SQLSTATEs，而不是 S00XX。 这样做是为了与开放组和 ISO 标准保持一致。 在许多情况下，映射不是一对一的，因为标准重新定义了多个 SQLSTATEs 的解释。  
  
 当*odbc 2.x 应用程序升级*到 odbc 3.x 应用程序时，必须将该*应用程序更改*为预期 odbc 1.x SQLSTATEs，而不*是 odbc 2.x* *SQLSTATEs。* 下表列出了每个*odbc 2.X* *SQLSTATE 映射*到的 odbc SQLSTATEs。  
  
 当 SQL_ATTR_ODBC_VERSION 环境特性设置为 SQL_OV_ODBC2 时，驱动程序将在调用**SQLGetDiagField**或**SQLGETDIAGREC**时发布 odbc 2.x SQLSTATEs，而不*是 odbc 1.x* *SQLSTATEs。* 可以通过在下表*的第 1*列中记下与第2列中的 odbc *2.x SQLSTATE 对应的 odbc* 2.x SQLSTATE 来确定具体的映射。  
  
|ODBC *2.X* SQLSTATE|ODBC *2.X* SQLSTATE|说明|  
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
|S1002|07009|如果基础函数为**SQLBindCol**、 **SQLColAttribute**、 **SQLExtendedFetch**、 **SQLFETCH**、 **SQLFetchScroll**或**SQLGetData**，则 odbc *2.x SQLSTATE S1002*将映射到 odbc 2.x *SQLSTATE 07009。*|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|为空指针的无效使用而返回。|  
|S1009|HY024|返回的属性值无效。|  
|S1009|HY092|当并发为只读**时，通过**调用**SQLSetPos**，或通过调用添加、更新或删除数据，返回以更新或删除数据。|  
|S1010|HY007 HY010|在调用 SQLDescribeCol、 **SQLPrepare**或*SQLExecDirect*的 Catalog 函数**之前调用** **STATEMENTHANDLE**时，SQLSTATE S1010 映射到 SQLSTATE HY007。 否则，SQLSTATE S1010 将映射到 SQLSTATE HY010。|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|如果基础函数是**SQLBindParameter**或**SQLDESCRIBEPARAM**，则 odbc *2.X SQLSTATE 07009 映射到 odbc 2.x* *SQLSTATE S1093* 。|  
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
>  ODBC *2.X SQLSTATE 07008 映射到 odbc 2.X* *SQLSTATE S1000* 。
