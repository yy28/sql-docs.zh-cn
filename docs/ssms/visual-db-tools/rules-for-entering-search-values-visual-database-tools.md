---
title: "用于输入搜索值的规则 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time [SQL Server], searches
- date searches
- dates [SQL Server], searches
- embedding apostrophes [SQL Server]
- logical value searches [SQL Server]
- case-sensitive search matches
- search criteria [SQL Server], rules
- text value searches [SQL Server]
- numeric value searches [SQL Server]
ms.assetid: 3c8134b7-83f4-41b4-99c8-e3949a685ff5
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 979bc40803391e773624d9d7f2b9e43e3bad5ee6
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="rules-for-entering-search-values-visual-database-tools"></a>输入搜索值的规则 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 本主题讨论当为搜索条件输入以下类型的文本值时必须遵循的约定：  
  
-   文本值  
  
-   数值  
  
-   日期  
  
-   逻辑值  
  
> [!NOTE]  
> 本主题中的信息派生自标准 SQL-92 的规则。 但是，每个数据库能够以自己的方式实现 SQL。 因此，这里提供的准则不一定适用于每一种情况。 如果在如何为某个数据库输入搜索值方面有任何疑问，请参阅您所使用的数据库文档。  
  
## <a name="searching-on-text-values"></a>搜索文本值  
以下准则适用于在搜索条件中输入文本值时的情况：  
  
-   **引号** 将文本值放到单引号内，如下例中的姓氏：  
  
    ```  
    'Smith'  
    ```  
  
    如果在 [条件窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中输入搜索条件，则只需键入文本值，查询和视图设计器将自动为该值括上单引号。  
  
    > [!NOTE]  
    > 在某些数据库中，单引号内的项被解释为文本值，而双引号内的项被解释为数据库对象，如列引用或表引用。 因此，尽管查询和视图设计器能够接受双引号中的项，但对其所做的解释有可能与您预期的不同。  
  
-   **嵌入的撇号** 如果搜索的数据包含一个单引号（撇号），则可以输入两个单引号以指示该单引号是文本值而非分隔符。 例如，下面的条件将搜索值“Swann's Way”：  
  
    ```  
    ='Swann''s Way'  
    ```  
  
-   **长度限制** 当输入长字符串时，不要超过数据库 SQL 语句的最大长度。  
  
-   **区分大小写** 遵循所用数据库大小写区分规则。 所使用的数据库决定文本搜索是否区分大小写。 例如，某些数据库将运算符“=”解释为精确区分大小写匹配，而有些数据库则允许匹配任意大写和小写字符组合。  
  
    如果不能确定数据库是否使用区分大小写搜索，可以在搜索条件中使用 UPPER 或 LOWER 函数转换搜索数据的大小写，如下例所示：  
  
    ```  
    WHERE UPPER(lname) = 'SMITH'  
    ```  
  
## <a name="searching-on-numeric-values"></a>搜索数值  
以下准则适用于在搜索条件中输入数值时的情况：  
  
-   **引号** 不能将数字放在引号内。  
  
-   **非数字字符** 除小数点分隔符（在 Windows 控制面板的“区域设置”对话框中定义）和负号 (-) 之外，不能包含非数字字符。 不能包含数字分组符号（如千位间的逗号）或货币符号。  
  
-   **小数点标记** 如果输入整数，则可以包含小数点标记，无论所搜索的值是整数还是实数。  
  
-   **科学记数法** 可以使用科学记数法输入非常大或非常小的数字，如下例所示：  
  
    ```  
    > 1.23456e-9  
    ```  
  
## <a name="searching-on-dates"></a>搜索日期  
用来输入日期的格式取决于所使用的数据库和在查询和视图设计器的哪个窗格中输入日期。  
  
> [!NOTE]  
> 如果不知道数据源所使用的格式，请在“条件”窗格的筛选器列中以您所熟悉的任何格式输入日期。 设计器会将大多数这样的输入转换为正确的格式。  
  
查询和视图设计器可以使用以下日期格式：  
  
-   **区域设置特定** 在“Windows 区域设置属性”对话框中指定的日期格式。  
  
-   **数据库特定** 数据库可以理解的任何格式。  
  
-   **ANSI 标准日期** 使用大括号、标记“d”指定日期和日期字符串的格式，如下例所示：  
  
    ```  
    { d '1990-12-31' }  
    ```  
  
-   **ANSI 标准日期时间** 与 ANSI 标准日期相似，但用“ts”代替“d”，并在日期中添加小时、分钟和秒（使用 24 小时制），如下例中的 1990 年 12 月 31 日：  
  
    ```  
    { ts '1990-12-31 00:00:00' }  
    ```  
  
    通常，ANSI 标准日期格式用于那些使用真实日期数据类型表示日期的数据库。 相反，日期时间格式用于支持 datetime 数据类型的数据库。  
  
下表汇总了可在查询和视图设计器的不同窗格中使用的日期格式：  
  
|**窗格**|**日期格式**|  
|------------|-------------------|  
|条件|区域设置特定、数据库特定、ANSI 标准<br /><br />在 [条件窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) 中输入的日期将在 SQL 窗格中转换成与数据库兼容的格式。|  
|SQL|数据库特定、ANSI 标准|  
|结果|区域设置特定|  
  
## <a name="searching-on-logical-values"></a>搜索逻辑值  
逻辑数据的格式因数据库而异。 False 值通常存储为零 (0)。 True 值通常存储为 1，有时存储为 -1。 以下准则适用于在搜索条件中输入逻辑值时的情况：  
  
-   若要搜索 False 值，请使用零，如下例所示：  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 0  
    ```  
  
-   如果在搜索 True 值时不能确定使用什么格式，可尝试使用 1，如下例所示：  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 1  
    ```  
  
-   或者，也可以通过搜索任何非零值来扩大搜索范围，如下例所示：  
  
    ```  
    SELECT * FROM authors  
    WHERE contract <> 0  
    ```  
  
## <a name="see-also"></a>另请参阅  
[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
