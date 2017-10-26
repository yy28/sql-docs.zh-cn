---
title: "处理 SQL 语句 |Microsoft 文档"
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
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3613775e14453c2ed14e70cf122bd527217b2cd7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="processing-sql-statements"></a>处理 SQL 语句
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 ODBC 游标库所有 SQL 语句将直接都传递到除以下驱动程序：  
  
-   定位更新和 delete 语句  
  
-   **选择更新**语句  
  
-   批处理的 SQL 语句  
  
 若要执行的定位的更新和 delete 语句并将光标置于要调用的行**SQLGetData**该行，光标库构造标识行的搜索的语句。  
  
 本部分包含以下主题。  
  
-   [处理定位 Update 和 Delete 语句](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [处理 UPDATE 语句的选择](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [处理批次的 SQL 语句](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)

