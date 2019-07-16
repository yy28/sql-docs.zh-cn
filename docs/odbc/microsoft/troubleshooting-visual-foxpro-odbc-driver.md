---
title: 疑难解答 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4eeb6210b9bce124e16a1b4e666dee03c1d992be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912385"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>疑难解答（Visual FoxPro ODBC 驱动程序）
以下部分介绍如何提高性能并解决使用 Visual FoxPro ODBC 驱动程序时可能遇到的问题。  
  
## <a name="accessing-parameterized-views"></a>访问参数化的视图  
 无法访问 Visual FoxPro 数据库使用的驱动程序中的参数化的视图。 参数化的视图在视图的 SQL 中创建的 WHERE 子句**选择**语句限制记录的下载到满足条件的 WHERE 子句中使用提供的值的参数生成这些记录。 驱动程序不支持将参数传递给视图，因为尝试访问参数化的视图通过使用该驱动程序将失败。  
  
 可以在运行时提供或以编程方式传递给视图的参数值。  
  
## <a name="accessing-remote-views"></a>访问远程视图  
 无法访问 Visual FoxPro 数据库使用的驱动程序中的远程视图。 远程视图是访问非 FoxPro 数据或 FoxPro 和非 FoxPro 数据的组合的视图。 若要访问远程视图，请使用 Visual FoxPro。  
  
## <a name="deleting-records"></a>删除记录  
 您可以将记录标记为待删除使用该驱动程序，但您不能从数据库中永久删除记录。 若要永久删除表中的记录，请使用 Visual FoxPro。  
  
## <a name="increasing-performance-using-background-fetching"></a>增加使用背景提取性能  
 可以通过使用提取的驱动程序的功能在后台提高大型提取操作的性能。 背景提取使用单独的线程来提取从特定的数据源请求数据。  
  
 您可以使用背景提取的数据源中的以下方法之一：  
  
-   检查**提取背景中的数据**上的复选框[ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)。  
  
-   在连接字符串中使用 BackgroundFetch 属性关键字。  
  
 有关连接字符串属性关键字的信息，请参阅[连接字符串使用](../../odbc/microsoft/using-connection-strings.md)。  
  
## <a name="updating-multitiered-views"></a>更新多层视图  
 多层视图是根据一个或多个视图而不是基表的视图。 多层视图中的数据更新时，更新转下只有一个级别，到在所基于的顶级视图; 视图不会更新基表。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>在存储过程中使用数据定义语言 (DDL)  
 Visual FoxPro 存储过程中，不能使用 DDL，例如 CREATE TABLE 或 ALTER TABLE。  
  
 可以在存储过程中使用的语言的信息，请参阅[规则、 触发器、 默认值和存储过程支持](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)。  
  
## <a name="using-positioned-updates"></a>使用定位的更新  
 驱动程序不支持定位的更新。 使用 SQL WHERE 子句来标识你想要更新的行。  
  
## <a name="using-the-set-ansi-command"></a>使用 SET ANSI 命令  
 如果你是 Visual FoxPro 开发人员，应注意设置 ANSI 的默认设置对于该驱动程序，与默认设置为 OFF Visual FoxPro 相比是 ON。 有关设置 ANSI 设置上的默认值允许 Visual FoxPro 数据源与通常执行精确比较其他 ODBC 数据源中行为一致。 您可以更改默认设置。 有关详细信息，请参阅[设置 ANSI](../../odbc/microsoft/set-ansi-command.md)。
