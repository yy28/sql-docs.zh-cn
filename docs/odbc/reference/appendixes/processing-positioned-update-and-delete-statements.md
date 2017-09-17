---
title: "处理定位 Update 和 Delete 语句 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 367062f5e671b366771b1a04f129b8e312f48cca
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="processing-positioned-update-and-delete-statements"></a>处理定位 Update 和 Delete 语句
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库支持定位更新和 delete 语句，通过替换**WHERE CURRENT OF**中与此类语句子句**其中**枚举其缓存中存储的值的子句每个绑定的列。 游标库传递新构造**更新**和**删除**的驱动程序执行的语句。 对于定位的更新语句，游标库然后更新其缓存中的行集缓冲区中的值，并将相应的值设置到 SQL_ROW_UPDATED 行状态数组中。 为定位的 delete 语句，它到 SQL_ROW_DELETED 行状态数组中设置相应的值。  
  
> [!CAUTION]  
>  **其中**子句通过游标库来标识当前行构造可能无法识别的任何行，标识不同的行，或标识多个行。 有关详细信息，请参阅[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)、 本附录内容更高版本。  
  
 定位 update 和 delete 语句受到以下限制：  
  
-   定位 update 和 delete 语句可以使用仅在以下情况： 时**选择**语句生成的结果集; 当**选择**语句不包含联接， **联合**子句，或**GROUP BY**子句; 当使用一个别名或表达式选择列表中的任何列已与未绑定， **SQLBindCol**。  
  
-   如果应用程序准备定位的更新或删除语句，它必须之后执行此操作该维度被称为**SQLFetch**或**SQLFetchScroll**。 尽管游标库提交到的驱动程序准备的语句，它将关闭语句并执行它，直接在应用程序调用**SQLExecute**。  
  
-   如果该驱动程序支持只有一个活动语句，光标库提取的结果的其余部分设置，然后 refetches 从其缓存的当前行集之前执行的定位更新或删除语句。 如果应用程序然后调用一个返回结果集中的元数据函数 (例如， **SQLNumResultCols**或**SQLDescribeCol**)，游标库返回错误。  
  
-   如果定位的更新或删除语句执行包含每次执行更新时不自动更新的时间戳列的表的列，则所有后续定位的 update 或 delete 语句将失败的时间戳列是否绑定。 这是因为搜索更新或删除的是光标库创建的语句将不会准确地识别要更新的行。 时间戳列的搜索语句中的值将不匹配的时间戳列自动更新后的值。
