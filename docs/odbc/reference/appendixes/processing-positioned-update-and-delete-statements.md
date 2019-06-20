---
title: 处理定位更新和删除语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d898fcc7d1b35230173afa0443219d59c54720ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057070"
---
# <a name="processing-positioned-update-and-delete-statements"></a>处理定位更新和删除语句
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库支持定位更新和 delete 语句替换**WHERE CURRENT OF**子句中使用此类语句**其中**枚举其缓存中存储的值的子句每个绑定的列。 游标库传递新构造**更新**并**删除**语句来执行的驱动程序。 对于定位的更新语句，游标库然后更新其缓存中的行集缓冲区的值并设置到 SQL_ROW_UPDATED 的行状态数组中的相应值。 对于定位的 delete 语句，它为 SQL_ROW_DELETED 行状态数组中设置相应的值。  
  
> [!CAUTION]  
>  **其中**子句通过游标库来标识当前行来构造可能无法识别的任何行，标识不同的行，或标识多个行。 有关详细信息，请参阅[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)、 本附录中更高版本。  
  
 定位 update 和 delete 语句受到以下限制：  
  
-   定位 update 和 delete 语句仅在以下情况下使用： 当**选择**生成结果集的语句; 当**选择**语句未包含一个联接， **UNION**子句，或**分组依据**子句; 和选择列表中使用了别名或表达式的任何列时未绑定与**SQLBindCol**。  
  
-   如果应用程序准备定位的 update 或 delete 语句，它必须后执行此操作这一操作称作**SQLFetch**或**SQLFetchScroll**。 尽管游标库提交到准备的驱动程序语句时，它将关闭语句并执行它直接在应用程序调用**SQLExecute**。  
  
-   如果该驱动程序支持只有一个活动语句，游标库获取结果的其余部分设置，然后 refetches 从其缓存到当前行之前执行定位更新或删除语句。 如果应用程序然后调用一个函数，在结果集中返回的元数据 (例如， **SQLNumResultCols**或**SQLDescribeCol**)，该游标库将返回错误。  
  
-   如果定位的 update 或 delete 语句执行包含每次在执行更新时自动更新的时间戳列的表的列，则所有后续的定位的更新或删除语句将失败的时间戳列是否绑定。 这是因为搜索更新或删除游标库创建语句将不会准确地识别要更新的行。 时间戳列搜索语句中的值将与时间戳列的自动更新后的值不匹配。
