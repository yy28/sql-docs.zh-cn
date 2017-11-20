---
title: "构造搜索语句 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 90464acc97539252ae24aa6f959c16f58465d715
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="constructing-searched-statements"></a>构造搜索语句
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 若要支持定位的更新和 delete 语句，光标库构造搜索**更新**或**删除**从定位语句的语句。 以支持对调用**SQLGetData**的数据块中的是光标库构造搜索**选择**语句创建的结果集包含数据的当前行。 在上述每个语句，**其中**子句枚举的值存储在缓存中用于每个绑定的列中的 SQL_DESC_SEARCHABLE 字段标识符返回 SQL_PRED_SEARCHABLE 或 SQL_PRED_BASIC **SQLColAttribute**。  
  
> [!CAUTION]  
>  **其中**子句通过游标库来标识当前行构造可能无法识别的任何行，标识不同的行，或标识多个行。  
  
 如果定位的更新或删除语句影响到多个行，光标库将更新的行状态数组仅在其光标定位并返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （游标操作冲突） 的行。 如果语句未发现任何行，光标库不会更新行状态数组，并返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （游标操作冲突）。 应用程序可以调用**SQLRowCount**以确定已更新或删除的行数。  
  
 如果**选择**子句用于对的调用将光标**SQLGetData**标识多个行， **SQLGetData**不保证能够返回正确的数据。 如果它不会确定任何行， **SQLGetData**返回 SQL_NO_DATA。  
  
 如果应用程序符合以下指导原则，**其中**子句通过游标库构造应单独标识当前行，除非这是不可能，例如当数据源包含重复行。  
  
-   **绑定可唯一标识一行的列。** 如果绑定的列不能唯一标识行**其中**子句通过游标库构造可能标识多个行。 定位的更新或删除语句中，在这样的子句可能导致多个要更新或删除的行。 对的调用中**SQLGetData**，这样的子句可能会导致要返回的错误的行的数据的驱动程序。 中的唯一键绑定所有列保证唯一标识每个行。  
  
-   **分配数据缓冲区足够大，不会发生截断。** 游标库的缓存是绑定到结果集的行集缓冲区中的值的副本**SQLBindCol**。 如果数据被截断放在这些缓冲区时，它将还被截断在缓存中。 A**其中**从截断值构造的子句可能无法正确标识数据源中的基础行。  
  
-   **指定非 null 长度的二进制 C 数据的缓冲区。** 游标库分配中其缓存才长度缓冲区*StrLen_or_IndPtr*中的参数**SQLBindCol**为非 null。 当*TargetType*自变量是 SQL_C_BINARY，光标库需要要构造的二进制数据的长度**其中**子句从数据。 如果没有长度缓冲区 SQL_C_BINARY 列和应用程序调用**SQLGetData**或尝试执行的定位的更新或删除语句，光标库返回 SQL_ERROR 和 SQLSTATE SL014 （定位发出请求，并不是所有的列计数字段已缓冲处理）。  
  
-   **指定非 null 长度缓冲区为 null 的列。** 游标库分配中其缓存才长度缓冲区*StrLen_or_IndPtr*中的参数**SQLBindCol**为非 null。 因为 SQL_NULL_DATA 存储长度缓冲区中，光标库假定没有长度对于指定缓冲区任何列是不可为 null。 如果可以为 null 的列指定没有长度列，则光标库构造**其中**使用列的数据值的子句。 此子句将无法正确标识行。

