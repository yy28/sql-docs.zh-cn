---
title: 故障排除（Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912385"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>疑难解答（Visual FoxPro ODBC 驱动程序）
以下各节介绍了如何提高性能并解决使用 Visual FoxPro ODBC 驱动程序时可能遇到的问题。  
  
## <a name="accessing-parameterized-views"></a>访问参数化视图  
 使用驱动程序时，不能访问 Visual FoxPro 数据库中的参数化视图。 参数化视图在视图的 SQL **SELECT**语句中创建 WHERE 子句，该子句将下载的记录限制为满足使用为参数提供的值生成的 WHERE 子句条件的记录。 由于驱动程序不支持将参数传递给视图，因此尝试使用驱动程序访问参数化视图将失败。  
  
 可以在运行时提供参数值，也可以通过编程方式将参数值传递给视图。  
  
## <a name="accessing-remote-views"></a>访问远程视图  
 使用驱动程序时，不能访问 Visual FoxPro 数据库中的远程视图。 远程视图是访问非 FoxPro 数据或 FoxPro 和非 FoxPro 数据的组合的视图。 若要访问远程视图，请使用 Visual FoxPro。  
  
## <a name="deleting-records"></a>删除记录  
 您可以使用驱动程序标记要删除的记录，但不能从数据库中永久删除记录。 若要永久删除表中的记录，请使用 Visual FoxPro。  
  
## <a name="increasing-performance-using-background-fetching"></a>使用背景提取提高性能  
 通过使用驱动程序的后台获取功能，可以提高大型提取的性能。 背景获取使用单独的线程来提取从特定数据源请求的数据。  
  
 可以通过以下方式之一使用数据源的背景获取：  
  
-   选中 " [ODBC Visual FoxPro 安装程序" 对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)中的 "**在后台提取数据**" 复选框。  
  
-   在连接字符串中使用 BackgroundFetch 特性关键字。  
  
 有关连接字符串属性关键字的信息，请参阅[使用连接字符串](../../odbc/microsoft/using-connection-strings.md)。  
  
## <a name="updating-multitiered-views"></a>更新各层视图  
 多层视图是基于一个或多个视图（而不是基表）的视图。 当你在多层视图中更新数据时，更新只会向下移动一个级别，指向顶级视图所基于的视图;不更新基表。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>在存储过程中使用数据定义语言（DDL）  
 在 Visual FoxPro 存储过程中，不能使用 DDL，例如 CREATE TABLE 或 ALTER TABLE。  
  
 有关可以在存储过程中使用的语言的信息，请参阅[对规则、触发器、默认值和存储过程的支持](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)。  
  
## <a name="using-positioned-updates"></a>使用定位更新  
 该驱动程序不支持定位更新。 使用 SQL WHERE 子句标识要更新的行。  
  
## <a name="using-the-set-ansi-command"></a>使用 SET ANSI 命令  
 如果您是 Visual FoxPro 开发人员，您应该注意到该驱动程序的 SET ANSI 的默认设置为 ON，而 Visual FoxPro 的默认设置为 OFF。 设置 ANSI 的默认 ON 设置允许 Visual FoxPro 数据源与通常执行完全比较的其他 ODBC 数据源的行为一致。 您可以更改默认设置。 有关详细信息，请参阅[SET ANSI](../../odbc/microsoft/set-ansi-command.md)。
