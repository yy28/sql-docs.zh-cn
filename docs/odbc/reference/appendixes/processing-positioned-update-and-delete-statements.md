---
title: 处理定位更新和删除语句 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b3f20da018bcd4e28e8ffca097fb5a4373d7f42
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308018"
---
# <a name="processing-positioned-update-and-delete-statements"></a>处理定位更新和删除语句
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 游标库支持定位更新和删除语句，将此类语句中的**WHERE CURRENT OF**子句替换为**WHERE**子句，该子句枚举每个绑定列在其缓存中存储的值。 游标库将**新构造的更新**和**DELETE**语句传递给驱动程序以执行。 对于定位的更新语句，游标库然后从行集缓冲区中的值更新其缓存，并将行状态数组中的相应值设置为SQL_ROW_UPDATED。 对于定位删除语句，它将行状态数组中的相应值设置为SQL_ROW_DELETED。  
  
> [!CAUTION]  
>  游标库为标识当前行而构造的**WHERE**子句可能无法标识任何行、标识其他行或标识多行。 有关详细信息，请参阅在此附录的后面部分[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 定位的更新和删除语句受以下限制：  
  
-   定位更新和删除语句只能在以下情况下使用：当 SELECT 语句生成结果集时;**当 SELECT**语句生成结果集时，才能使用定位更新和删除语句。当**SELECT**语句不包含联接 **、UNION**子句或 GROUP **BY**子句时;以及当在选择列表中使用别名或表达式的任何列未绑定**到 SQLBindCol**时。  
  
-   如果应用程序准备定位的更新或删除语句，则必须在调用**SQLFetch**或**SQLFetchScroll**后执行此操作。 尽管游标库将语句提交到驱动程序进行准备，但它关闭语句并在应用程序调用**SQLExecute**时直接执行该语句。  
  
-   如果驱动程序仅支持一个活动语句，则游标库将获取结果集的其余部分，然后在执行其定位的更新或删除语句之前从缓存中重新提取当前行集。 如果应用程序然后调用一个函数，该函数返回结果集中的元数据（例如 **，SQLNumResultCols**或**SQLDescribeCol），** 则游标库将返回错误。  
  
-   如果在表的列上执行定位更新或删除语句，该列包含每次执行更新时自动更新的时间戳列，则如果绑定时间戳列，则所有后续定位的更新或删除语句都将失败。 这是因为游标库创建的搜索的更新或删除语句无法准确标识要更新的行。 时间戳列的搜索语句中的值与时间戳列的自动更新值不匹配。
