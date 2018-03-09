---
title: "疑难解答 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1074d9134e9ee0c0b1a828debd225b1462e53c4a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>疑难解答 （Visual FoxPro ODBC 驱动程序）
以下各节讨论如何提高性能，并解决在使用 Visual FoxPro ODBC 驱动程序时可能遇到的问题。  
  
## <a name="accessing-parameterized-views"></a>访问参数化的视图  
 无法访问 Visual FoxPro 数据库使用的驱动程序中的参数化的视图。 参数化的视图创建 WHERE 子句在视图的 SQL**选择**限制的记录的语句下载到满足使用提供的值的参数生成 WHERE 子句条件的那些记录。 该驱动程序不支持将参数传递给视图，因为尝试访问的参数化的视图，使用驱动程序将会失败。  
  
 可以在运行时提供或以编程方式传递给视图的参数值。  
  
## <a name="accessing-remote-views"></a>访问远程视图  
 无法访问 Visual FoxPro 数据库使用的驱动程序中的远程视图。 远程视图是访问非 FoxPro 数据或 FoxPro 和非 FoxPro 数据的组合的视图。 若要访问远程视图，使用 Visual FoxPro。  
  
## <a name="deleting-records"></a>删除记录  
 你可以将记录标记为删除使用该驱动程序，但你无法从数据库中永久删除记录。 若要永久删除表中的记录，请使用 Visual FoxPro。  
  
## <a name="increasing-performance-using-background-fetching"></a>增加使用背景提取性能  
 可以通过使用后台提取的驱动程序的功能来提高大型提取的性能。 背景提取使用单独的线程来提取特定数据源从请求数据。  
  
 你可以采用背景提取的数据源中通过以下方式之一：  
  
-   检查**提取数据，在后台**上的复选框[ODBC Visual FoxPro 安装程序对话框中](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)。  
  
-   在你的连接字符串中使用 BackgroundFetch 属性关键字。  
  
 有关连接字符串属性关键字的信息，请参阅[使用连接字符串](../../odbc/microsoft/using-connection-strings.md)。  
  
## <a name="updating-multitiered-views"></a>更新多层视图  
 多层视图是基于一个或多个视图而非基于基础表的视图。 在更新多层视图中的数据时，更新停机仅一个级别，到在所基于的顶级视图; 视图不会更新基表。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>在存储过程中使用数据定义语言 (DDL)  
 Visual FoxPro 存储过程中，不能使用 DDL，例如 CREATE TABLE 或 ALTER TABLE。  
  
 可以使用存储过程中的语言的信息，请参阅[支持规则、 触发器、 默认值和存储过程](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)。  
  
## <a name="using-positioned-updates"></a>使用定位的更新  
 驱动程序不支持定位的更新。 使用 SQL WHERE 子句来标识你想要更新的行。  
  
## <a name="using-the-set-ansi-command"></a>使用 SET ANSI 命令  
 如果你是 Visual FoxPro 开发人员，应该注意设置 ANSI 的默认设置对于该驱动程序，与 Visual FoxPro 的 OFF 的默认设置是 ON。 设置 ANSI 设置上的默认值允许 Visual FoxPro 数据源，以与其他 ODBC 数据源，通常可以执行精确比较的行为保持一致。 你可以更改默认设置。 有关详细信息，请参阅[设置 ANSI](../../odbc/microsoft/set-ansi-command.md)。
