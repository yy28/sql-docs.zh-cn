---
title: 构造搜索语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 616e4241c6d28e846a56116a70e79254e13dd5fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224555"
---
# <a name="constructing-searched-statements"></a>构造搜索语句
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 若要支持定位的 update 和 delete 语句，该游标库构造搜索**更新**或**删除**中定位的语句的语句。 若要支持对调用**SQLGetData**中的数据块，游标库构造搜索**选择**语句来创建这样的结果集，其中包含数据的当前行。 在每个这些语句**其中**子句枚举的值存储在缓存中的每个绑定列中 SQL_DESC_SEARCHABLE 字段标识符返回 SQL_PRED_SEARCHABLE 或 SQL_PRED_BASIC **SQLColAttribute**。  
  
> [!CAUTION]  
>  **其中**子句通过游标库来标识当前行来构造可能无法识别的任何行，标识不同的行，或标识多个行。  
  
 如果定位的 update 或 delete 语句影响多个行，该游标库更新行状态数组仅对行的游标定位并返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （游标操作冲突）。 如果语句未标识任何行，游标库不会更新行状态数组，并返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （游标操作冲突）。 应用程序可以调用**SQLRowCount**来确定的已更新或删除的行数。  
  
 如果**选择**子句用于对的调用将光标置于**SQLGetData**标识多个行**SQLGetData**不保证能够返回正确的数据。 如果未标识任何行**SQLGetData**返回 sql_no_data 为止。  
  
 如果应用程序符合以下指导原则**其中**子句通过游标库构造应唯一标识当前行，除非这是不可能的例如，当数据源包含重复行。  
  
-   **将唯一标识行的列绑定。** 如果绑定的列不能唯一标识行**其中**子句通过游标库构造可能标识多个行。 在定位的 update 或 delete 语句中，这样的子句可能会导致多个要更新或删除的行。 在调用**SQLGetData**，这样的子句可能导致驱动程序返回的错误行的数据。 中的唯一键绑定所有列可保证唯一地标识每个行。  
  
-   **分配数据缓冲区足够大，不会发生截断。** 游标库缓存是绑定到结果集的行集缓冲区中的值的副本**SQLBindCol**。 如果放在这些缓冲区时，数据将被截断，它将还被截断在缓存中。 一个**其中**子句从截断的值构造可能不正确地标识数据源中的基础行。  
  
-   **指定用于 C 的二进制数据的非 null 长度缓冲区。** 游标库分配长度缓冲区在其缓存才*StrLen_or_IndPtr*中的参数**SQLBindCol**为非 null。 当*TargetType*参数为 SQL_C_BINARY 时，游标库需要的要构造的二进制数据的长度**其中**子句从数据。 如果没有为 SQL_C_BINARY 列和应用程序调用没有长度缓冲区**SQLGetData**或尝试执行定位的更新或删除语句，该游标库返回 SQL_ERROR 并且 SQLSTATE SL014 （定位发出请求，并不是所有的列计数字段已缓冲处理）。  
  
-   **指定非 null 长度缓冲区为 null 的列。** 游标库分配长度缓冲区在其缓存才*StrLen_or_IndPtr*中的参数**SQLBindCol**为非 null。 由于 SQL_NULL_DATA 存储在长度缓冲区，该游标库假定哪些没有长度限制为指定缓冲区的任何列不可为 null。 如果为空的列指定没有长度列，则该游标库构造**其中**列使用的数据值的子句。 此子句将不会正确识别行。
