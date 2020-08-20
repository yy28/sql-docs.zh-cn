---
description: 使用安装程序添加和修改数据源
title: 使用安装程序添加和修改数据源 |Microsoft Docs
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
ms.openlocfilehash: 8592c01897e691cdb6702c4efdfca6054655a793
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494737"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>使用安装程序添加和修改数据源
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 数据源标识包含网络库、服务器、数据库和其他属性（在本例中为数据源是 Oracle 数据库的路径）的数据的路径。 为了连接到数据源，驱动程序管理器会检查 Windows 注册表中是否有特定的连接信息。  
  
 Odbc 数据源管理器创建的注册表项由 ODBC 驱动程序管理器和 ODBC 驱动程序使用。 此条目包含有关每个数据源及其关联的驱动程序的信息。 在连接到数据源之前，必须将其连接信息添加到注册表中。  
  
 若要添加和配置数据源，请使用 [ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)。 ODBC 管理器更新您的数据源连接信息。 添加数据源时，ODBC 管理员会更新注册表信息。  
  
### <a name="to-add-a-data-source-for-windows"></a>为 Windows 添加数据源  
  
1.  打开 "ODBC 数据源管理器"。  
  
2.  在 "ODBC 数据源管理器" 对话框中，单击 "添加"。 此时将显示 "新建数据源" 对话框。  
  
3.  选择 "Microsoft ODBC for Oracle"，然后单击 "完成"。 此时将显示 "Microsoft ODBC for Oracle 设置" 对话框。  
  
4.  在 "数据源名称" 框中，键入要访问的数据源的名称。 它可以是你选择的任何名称。  
  
5.  在 "说明" 框中，键入驱动程序的说明。 此可选字段描述数据源连接到的数据库驱动程序。 它可以是你选择的任何名称。  
  
6.  在 "用户名" 框中，键入数据库用户名称 (数据库用户 ID) 。  
  
7.  在 "服务器" 框中，键入要访问的 Oracle 服务器引擎的数据库别名或连接字符串。  
  
8.  单击 "确定" 以添加此数据源。  
  
> [!NOTE]  
>  "数据源" 对话框将出现，ODBC 管理员会更新注册表信息。 当你连接到数据源时，你键入的用户名和连接字符串将成为此数据源的默认连接值。  
  
1.  单击 "选项" 以更好地了解用于 Oracle 的 ODBC 驱动程序安装程序：  
  
    -   **翻译** -单击 "选择" 以选择已加载的数据转换器。 默认值为 \<No Translator>。  
  
    -   **性能** -"在目录函数中包括备注" 复选框指定驱动程序是否为 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 结果集返回备注列。 如果未设置此值，则用于 Oracle 的 ODBC 驱动程序可提供更快的访问。  
  
         "在 SQL 列中包含同义词" 复选框指定驱动程序是否返回列信息。 **缓冲区大小** 指定分配用于接收提取的数据的大小（以字节为单位）。 驱动程序将优化提取，以便从 Oracle 服务器提取一次，以填充指定大小的缓冲区。 较大的值在提取大量数据时可能会提高性能。  
  
    -   **自定义** -"强制 ODBC DayOfWeek 标准" 复选框指定结果集是否符合 ODBC 指定的星期几格式 (星期日 = 1;星期六 = 7) 。 如果清除此复选框，则会返回特定于区域设置的 Oracle 值。  
  
         "SQLDescribeCol**始终返回值**" 复选框指定驱动程序是否应为**SQLDescribeCol**的*cbColDef*参数返回非零值。 此连接字符串属性仅适用于没有 Oracle 定义的刻度的列，例如，计算所得的数值列和定义为数值的列，无精度或小数位数。 当 Oracle 不提供该信息时， **SQLDescribeCol** 调用返回130的精度。 如果清除此复选框，则驱动程序将为这些类型的列返回0。  
  
2.  单击 "添加" 以添加另一个数据源，或者单击 "关闭" 以退出。  
  
### <a name="to-modify-a-data-source-for-windows"></a>修改 Windows 的数据源  
  
1.  打开 "ODBC 数据源管理器"。 单击相应的 DSN 选项卡。  
  
2.  选择要修改的 Oracle 数据源，然后单击 "配置"。 此时将显示 "Microsoft ODBC for Oracle 设置" 对话框。  
  
3.  修改适用的数据源字段，然后单击 "确定"。  
  
 完成修改此对话框中的信息后，ODBC 管理员会更新注册表信息。
