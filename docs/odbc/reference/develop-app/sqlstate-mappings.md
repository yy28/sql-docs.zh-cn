---
title: SQLSTATE 映射 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299737"
---
# <a name="sqlstate-mappings"></a>SQLSTATE 映射
本主题讨论 ODBC *2.x*和 ODBC *3.x*的 SQLSTATE 值。 有关 ODBC *3.x* SQLSTATE 值的详细信息，请参阅[附录 A：ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。  
  
 在 ODBC *3.x*中，将返回 HYxxx SQLSTATEs 而不是 S1xxx，返回 42Sxx SQLSTATEs 而不是 S00XX。 这样做是为了符合开放集团和 ISO 标准。 在许多情况下，映射不是一对一的，因为标准重新定义了对多个 SQLSTAT 的解释。  
  
 当 ODBC *2.x*应用程序升级到 ODBC *3.x*应用程序时，必须更改应用程序以预期 ODBC *3.x* SQLSTATEs 而不是 ODBC *2.x* SQLSTAT。 下表列出了每个 ODBC *2.x* SQLSTATE 映射到的 ODBC *3.x* SQLSTATEs。  
  
 当SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC2时，当调用**SQLGetDiagField**或**SQLGetDiagRec**时，驱动程序将发布 ODBC *2.x* SQLSTATEs 而不是 ODBC *3.x* SQLSTATEs。 可以通过记录下表第 1 列中对应于第 2 列中的 ODBC *3.x* SQLSTATE 的 ODBC *2.x* SQLSTATE 来确定特定的映射。  
  
|ODBC *2.x* SQLSTATE|ODBC *3.x* SQLSTATE|注释|  
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
|S1002|07009|如果基础函数是**SQLBindCol、SQLCol****属性****、SQL 扩展获取****、SQLFetch、SQLFetchScroll**或**SQLGetData，** 则 ODBC *2.x* SQLSTATE S1002 映射到 ODBC *3.x* SQLSTATE 07009。 **SQLFetchScroll**|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|返回以无效使用空指针。|  
|S1009|HY024|为无效的属性值返回。|  
|S1009|HY092|返回以更新或删除数据，通过调用**SQLSetPos**， 或通过调用**SQLBulk 操作**（当并发是只读的）添加、更新或删除数据。|  
|S1010|HY007 HY010|SQLSTATE S1010 映射到 SQLSTATE HY007，当**SQLDescribeCol**在调用**SQLPrepare、SQLExecDirect**或*语句句柄*的目录函数之前调用时。 **SQLExecDirect** 否则，SQLSTATE S1010 将映射到 SQLSTATE HY010。|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|如果基础函数是**SQLBind参数**或**SQLDescribeParam，** 则 ODBC *3.x* SQLSTATE 07009 映射到 ODBC *2.x* SQLSTATE S1093。|  
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
>  ODBC *3.x* SQLSTATE 07008 映射到 ODBC *2.x* SQLSTATE S1000。
