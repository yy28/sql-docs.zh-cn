---
title: 使用设置添加和修改数据源 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae76abc902e4687e5d9891871d7d5d60598b3abc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281407"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>使用安装程序添加和修改数据源
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 数据源标识可包含网络库、服务器、数据库和其他属性的数据路径 - 在这种情况下，数据源是 Oracle 数据库的路径。 要连接到数据源，驱动程序管理器将检查 Windows 注册表中的特定连接信息。  
  
 ODBC 数据源管理员创建的注册表项由 ODBC 驱动程序管理器和 ODBC 驱动程序使用。 此条目包含有关每个数据源及其关联的驱动程序的信息。 必须先将数据源连接到数据源之前，必须将其连接信息添加到注册表中。  
  
 要添加和配置数据源，请使用[ODBC 数据源管理员](../../odbc/admin/odbc-data-source-administrator.md)。 ODBC 管理员更新数据源连接信息。 添加数据源时，ODBC 管理员会为您更新注册表信息。  
  
### <a name="to-add-a-data-source-for-windows"></a>为 Windows 添加数据源  
  
1.  打开 ODBC 数据源管理员。  
  
2.  在 ODBC 数据源管理员对话框中，单击"添加"。 此时将显示"创建新数据源"对话框。  
  
3.  为 Oracle 选择 Microsoft ODBC，然后单击"完成"。 将显示 Oracle 设置的 Microsoft ODBC 对话框。  
  
4.  在"数据源名称"框中，键入要访问的数据源的名称。 它可以是您选择的任何名称。  
  
5.  在"描述"框中，键入驱动程序的说明。 此可选字段描述数据源连接到的数据库驱动程序。 它可以是您选择的任何名称。  
  
6.  在"用户名"框中，键入数据库用户名（数据库用户 ID）。  
  
7.  在"服务器"框中，键入要访问的 Oracle 服务器引擎的数据库别名或连接字符串。  
  
8.  单击"确定"以添加此数据源。  
  
> [!NOTE]  
>  将显示"数据源"对话框，ODBC 管理员将更新注册表信息。 当您连接到该数据源时，您键入的用户名和连接字符串将成为此数据源的默认连接值。  
  
1.  单击"选项"可针对 Oracle 设置对 ODBC 驱动程序做出更多规范：  
  
    -   **翻译**- 单击"选择"以选择加载的数据转换器。 默认值为\<"无翻译人员>。  
  
    -   **性能**- 目录函数中的"包含注释"复选框指定驱动程序是否返回[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)结果集的备注列。 未设置此值时，Oracle 的 ODBC 驱动程序可提供更快的访问。  
  
         SQL 列中的"包括 SYNONYMS"复选框指定驱动程序是否返回列信息。 **缓冲区大小**指定分配给接收提取数据的大小（以字节为单位）。 驱动程序优化提取，以便从 Oracle 服务器提取的行返回足够的行来填充指定大小的缓冲区。 获取大量数据时，值越大，性能也会提高。  
  
    -   **自定义**- 强制 ODBC DayOfWeek 标准复选框指定结果集是否符合 ODBC 指定的周日格式（周日 = 1;星期六 = 7）。 如果清除此复选框，则返回特定于区域设置的 Oracle 值。  
  
         SQLDescribeCol**始终返回精度值**复选框，指定驱动程序是否应返回**SQLDescribeCol**的*cbColDef*参数的非零值。 此连接字符串属性仅适用于没有 Oracle 定义比例的列，例如计算的数字列和定义为 NUMBER 的列，没有精度或比例。 当 Oracle 不提供该信息时 **，SQLDescribeCol**调用返回 130 的精度。 如果清除此复选框，驱动程序将返回这些类型的列 0。  
  
2.  单击"添加"可添加其他数据源，或单击"关闭以退出"。  
  
### <a name="to-modify-a-data-source-for-windows"></a>修改 Windows 的数据源  
  
1.  打开 ODBC 数据源管理员。 单击相应的 DSN 选项卡。  
  
2.  选择要修改的 Oracle 数据源，然后单击"配置"。 将显示 Oracle 设置的 Microsoft ODBC 对话框。  
  
3.  修改适用的数据源字段，然后单击"确定"。  
  
 完成此对话框中的信息修改后，ODBC 管理员将更新注册表信息。
