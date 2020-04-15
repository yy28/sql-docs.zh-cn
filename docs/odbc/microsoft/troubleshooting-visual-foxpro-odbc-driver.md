---
title: 故障排除（可视化福克斯Pro ODBC驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b035069c0be88d05a3aa5e17b96af991c27405
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303028"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>疑难解答（Visual FoxPro ODBC 驱动程序）
以下各节讨论如何提高性能和解决您在使用 Visual FoxPro ODBC 驱动程序时可能遇到的问题。  
  
## <a name="accessing-parameterized-views"></a>访问参数化视图  
 无法使用驱动程序访问 Visual FoxPro 数据库中的参数化视图。 参数化视图在视图的 SQL **SELECT**语句中创建 WHERE 子句，该语句将下载的记录限制为满足使用为参数提供的值生成的 WHERE 子句的条件的记录。 由于驱动程序不支持将参数传递到视图，因此使用驱动程序访问参数化视图的尝试将失败。  
  
 参数值可以在运行时提供，也可以以编程方式传递到视图。  
  
## <a name="accessing-remote-views"></a>访问远程视图  
 无法使用驱动程序访问 Visual FoxPro 数据库中的远程视图。 远程视图是访问非 FoxPro 数据或 FoxPro 和非 FoxPro 数据组合的视图。 要访问远程视图，请使用 Visual FoxPro。  
  
## <a name="deleting-records"></a>删除记录  
 您可以使用驱动程序标记记录以进行删除，但不能从数据库中永久删除记录。 要从表中永久删除记录，请使用 Visual FoxPro。  
  
## <a name="increasing-performance-using-background-fetching"></a>使用后台提取提高性能  
 您可以使用驱动程序的背景提取功能提高大型提取的性能。 后台提取使用单独的线程从特定数据源获取请求的数据。  
  
 您可以通过以下方式之一对数据源使用后台提取：  
  
-   选中[ODBC 可视化 FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)上的**后台复选框中的"提取数据**"。  
  
-   在连接字符串中使用背景提取属性关键字。  
  
 有关连接字符串属性关键字的信息，请参阅[使用连接字符串](../../odbc/microsoft/using-connection-strings.md)。  
  
## <a name="updating-multitiered-views"></a>更新多层视图  
 多层视图是基于一个或多个视图而不是基表的视图。 更新多层视图中的数据时，更新只会向下到顶级视图所基于的视图，更新只会向下。基表不会更新。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>在存储过程中使用数据定义语言 （DDL）  
 在 Visual FoxPro 存储过程中，不能使用 DDL，例如创建表或 ALTER TABLE。  
  
 有关可在存储过程中使用的语言的信息，请参阅[支持规则、触发器、默认值和存储过程](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)。  
  
## <a name="using-positioned-updates"></a>使用定位更新  
 驱动程序不支持定位更新。 使用 SQL WHERE 子句标识要更新的行。  
  
## <a name="using-the-set-ansi-command"></a>使用 SET ANSI 命令  
 如果您是 Visual FoxPro 开发人员，您应该注意，SET ANSI 的默认设置是驱动程序的"打开"，这与 Visual FoxPro 的默认设置 OFF 相反。 SET ANSI 的默认设置允许 Visual FoxPro 数据源与其他通常执行精确比较的 ODBC 数据源保持一致。 您可以更改默认设置。 有关详细信息，请参阅[SET ANSI](../../odbc/microsoft/set-ansi-command.md)。
