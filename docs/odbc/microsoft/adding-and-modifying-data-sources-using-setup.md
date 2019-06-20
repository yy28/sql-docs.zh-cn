---
title: 添加和修改数据源使用安装程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 953563285d3c62a8523079a604cf607f2e0edf62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63219111"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>使用安装程序添加和修改数据源
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 数据源标识可以包含网络库、 服务器、 数据库和其他属性的数据的路径-在这种情况下，数据源是 Oracle 数据库的路径。 若要连接到数据源，驱动程序管理器，请检查 Windows 注册表中为特定的连接信息。  
  
 创建 ODBC 数据源管理器的注册表条目使用的 ODBC 驱动程序管理器和 ODBC 驱动程序。 此条目包含有关每个数据源和其关联的驱动程序的信息。 可以连接到数据源之前，必须向注册表添加其连接信息。  
  
 若要添加和配置数据源，请使用[ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)。 ODBC 管理器更新你的数据源连接信息。 添加数据源时，ODBC 管理器将更新为你的注册表信息。  
  
### <a name="to-add-a-data-source-for-windows"></a>若要为 Windows 添加数据源  
  
1.  打开 ODBC 数据源管理器。  
  
2.  在 ODBC 数据源管理器对话框中，单击添加。 创建新的数据源对话框。  
  
3.  选择适用于 Oracle 的 Microsoft ODBC，然后单击完成。 Microsoft ODBC Oracle 安装程序对话框将出现。  
  
4.  在数据源名称框中，键入你想要访问的数据源的名称。 它可以是任何您选择的名称。  
  
5.  在描述框中，键入该驱动程序的说明。 此可选字段描述数据源连接到的数据库驱动程序。 它可以是任何您选择的名称。  
  
6.  在用户名框中，键入数据库的用户名称 (您数据库的用户 ID)。  
  
7.  在服务器框中，键入数据库别名或连接你想要访问的 Oracle 服务器引擎的字符串。  
  
8.  单击确定以添加此数据源。  
  
> [!NOTE]  
>  数据源对话框中显示，且 ODBC 管理器更新的注册表信息。 用户名称和连接您键入的字符串连接到它时将成为此数据源的默认连接值。  
  
1.  单击选项进行更多有关 Oracle 安装程序的 ODBC 驱动程序规范：  
  
    -   **翻译**-单击选择选择加载的数据转换器。 默认值是\<否转换器 >。  
  
    -   **性能**-包括备注中目录函数复选框指定是否驱动程序将返回备注的列[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)结果集。 Oracle ODBC 驱动程序提供更快地访问时不设置此值。  
  
         SQL 列复选框中的包括同义词指定驱动程序是否返回列信息。 **缓冲区大小**指定的大小，以分配的字节数，以接收提取的数据。 该驱动程序可优化提取，以便从 Oracle 服务器的一个提取都将返回足够行来填充指定大小的缓冲区。 较大的值往往提取大量数据时提高性能。  
  
    -   **自定义**-强制实施 ODBC DayOfWeek 标准复选框指定结果集将遵从为 ODBC 指定一周中日期的格式 （星期日 = 1;星期六 = 7）。 如果清除此复选框，则返回特定于区域设置的 Oracle 值。  
  
         SQLDescribeCol**始终返回值的精度**复选框指定驱动程序是否应返回非零值*cbColDef*自变量的**SQLDescribeCol**. 此连接字符串属性仅适用于其中没有任何 Oracle 定义的小数位，如计算数值的列的列和列定义为数值，而无需精度或小数位数。 一个**SQLDescribeCol** Oracle 不提供该信息时，调用返回 130 的精度。 如果清除此复选框，则该驱动程序将改为返回这些类型的列 0。  
  
2.  单击添加以添加另一个数据源，或单击关闭退出。  
  
### <a name="to-modify-a-data-source-for-windows"></a>若要修改的数据源的 Windows  
  
1.  打开 ODBC 数据源管理器。 单击相应的 DSN 选项卡。  
  
2.  选择你想要修改，然后单击配置的 Oracle 数据源。 Microsoft ODBC Oracle 安装程序对话框将出现。  
  
3.  修改适用的数据源字段，然后单击确定。  
  
 完成修改此对话框中的信息，ODBC 管理器将更新的注册表信息。
