---
title: 构造搜索语句 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8b9a27aa9fc84aadc6659993de3e12e269631d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284737"
---
# <a name="constructing-searched-statements"></a>构造搜索语句
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 为了支持定位更新和删除语句，游标库从定位语句**构造搜索的更新**或**DELETE**语句。 为了支持对数据块中的**SQLGetData**的调用，游标库构造一个搜索的**SELECT**语句以创建包含当前数据行的结果集。 在每一个语句中 **，WHERE**子句都会枚举存储在缓存中为每个绑定列的值，这些值返回**SQLColAttribute**中SQL_DESC_SEARCHABLE字段标识符的SQL_PRED_SEARCHABLE或SQL_PRED_BASIC。  
  
> [!CAUTION]  
>  游标库为标识当前行而构造的**WHERE**子句可能无法标识任何行、标识其他行或标识多行。  
  
 如果定位的更新或删除语句影响多行，游标库仅针对游标所定位的行更新行状态数组，并返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01001（Cursor 操作冲突）。 如果语句未标识任何行，则游标库不会更新行状态数组，并返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01001（Cursor 操作冲突）。 应用程序可以调用**SQLRowCount**来确定更新或删除的行数。  
  
 如果用于定位**SQLGetData**调用的游标的**SELECT**子句标识了多行，则**SQLGetData**不保证返回正确的数据。 如果**SQLGetData**未识别任何行，则返回SQL_NO_DATA。  
  
 如果应用程序符合以下准则，则游标库构造的**WHERE**子句应唯一标识当前行，除非这是不可能的，例如数据源包含重复行时。  
  
-   **绑定唯一标识行的列。** 如果绑定列不唯一标识该行，则游标库构造的**WHERE**子句可能会标识多行。 在定位的更新或删除语句中，此类子句可能会导致更新或删除多行。 在调用**SQLGetData**时，此类子句可能会导致驱动程序返回错误行的数据。 将所有列绑定到唯一的键中，可确保每行都唯一标识。  
  
-   **分配足够大的数据缓冲区，以便不发生截断。** 游标库的缓存是使用**SQLBindCol**绑定到结果集的行集缓冲区中的值的副本。 如果数据被截断，当它被放置在这些缓冲区中时，它也会被截断在缓存中。 由截断值构造的**WHERE**子句可能无法正确标识数据源中的基础行。  
  
-   **为二进制 C 数据指定非空长度缓冲区。** 仅当**SQLBindCol**中的*StrLen_or_IndPtr*参数为非空时，游标库才会在其缓存中分配长度缓冲区。 当*TargetType*参数SQL_C_BINARY时，游标库需要二进制数据的长度才能从数据构造**WHERE**子句。 如果SQL_C_BINARY列没有长度缓冲区，并且应用程序调用**SQLGetData**或尝试执行定位的更新或删除语句，则游标库将返回SQL_ERROR和 SQLSTATE SL014（已发出定位请求，并非所有列计数字段都已缓冲）。  
  
-   **为空列指定非空长度缓冲区。** 仅当**SQLBindCol**中的*StrLen_or_IndPtr*参数为非空时，游标库才会在其缓存中分配长度缓冲区。 由于SQL_NULL_DATA存储在长度缓冲区中，因此游标库假定未为其指定长度缓冲区的任何列都是不可虚无的。 如果未为空列指定长度列，则游标库将构造一个**WHERE**子句，该子句使用列的数据值。 此子句无法正确标识该行。
