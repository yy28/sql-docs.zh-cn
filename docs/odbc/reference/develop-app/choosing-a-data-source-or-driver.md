---
title: "选择数据源或驱动程序 |Microsoft 文档"
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
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 496b9a40dfa1beb27144eead8d8ab9b03056b000
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="choosing-a-data-source-or-driver"></a>选择数据源或驱动程序
此数据源或应用程序使用的驱动程序，有时应用程序中硬编码。 例如，编写由 MIS 部门要传输到另一个数据源的数据将包含这些数据源的名称的自定义应用程序-应用程序只需将不起作用的任何其他数据源。 另一个示例是垂直的应用程序，例如另一个用于订单条目。 此类应用程序始终使用同一数据源，已由应用程序已知的预定义的架构。  
  
 其他应用程序在运行时选择此数据源或驱动程序。 通常情况下，它们是执行即席查询，如电子表格使用 ODBC 来导入数据的泛型应用程序。 通常，此类应用程序列出的可用数据源或驱动程序，并让用户选择他们的想要使用。 是否通用的应用程序列出数据源和 / 或驱动程序，经常取决于应用程序是否使用基于 DBMS 的或基于文件的驱动程序。  
  
 基于 DBMS 的驱动程序通常需要一组复杂的连接信息，如网络地址、 网络协议、 数据库名称和等等。 数据源的目的是隐藏的所有此信息。 因此，数据源范例适用于其自己以使用基于 DBMS 的驱动程序。 应用程序可在两种方式之一向用户显示数据源的列表。 它可以调用**SQLDriverConnect**与**DSN** （数据源名称） 关键字和任何关联的值; 驱动程序管理器将显示数据源名称的列表。 如果应用程序想要对列表的外观进行控制，则会调用**SQLDataSources**若要检索的一组可用数据源，并构造自己的对话框。 此函数实现通过驱动程序管理器，并且可以在调用之前任何驱动程序已加载。 然后，应用程序调用连接函数，并将其传递选的数据源的名称。  
  
 如果未指定数据源，则使用由系统信息的默认数据源。 (有关详细信息，请参阅[默认子项](../../../odbc/reference/install/default-subkey.md)。)如果**SQLConnect**调用通过使用*ServerName*找不到、 为 null 指针，或为"DEFAULT"的参数，驱动程序管理器连接到默认数据源。 对的调用中使用的连接字符串，也将使用数据源默认**SQLDriverConnect**或**SQLBrowseConnect**包含**DSN**关键字设置为"默认值"或如果找不到指定的数据源。 此外，对的调用中使用的连接字符串，如果使用数据源，则默认**SQLDriverConnect**不包含**DSN**关键字。  
  
 基于文件的驱动程序后，则可以使用文件范例。 对于存储在本地计算机上的数据，用户经常知道其数据在特定的文件中，如 Employee.dbf。 而不是选择未知的数据源时，它是此类用户选择他们所熟悉的文件更容易。 若要实现此操作，请在应用程序的第一个调用**SQLDrivers**。 此函数实现通过驱动程序管理器，并且可以在调用之前任何驱动程序已加载。 **SQLDrivers**返回列表的可用驱动程序; 它还返回的值**FileUsage**和**FileExtns**关键字。 **FileUsage**关键字说明是否基于文件的驱动程序将文件视为表，不 Xbase，或作为数据库，作为未 Microsoft® Access。 **FileExtns**关键字列出的文件扩展名，则驱动程序识别，例如.dbf Xbase 驱动程序。 应用程序使用此信息，构造对话框中，通过该用户选择一个文件。 基于所选的文件的扩展，然后，应用程序连接到该驱动程序通过调用**SQLDriverConnect**与**驱动程序**关键字。  
  
 没有要停止从数据源使用基于文件的驱动程序或调用应用程序内容**SQLDriverConnect**与**驱动程序**关键字来连接到基于 DBMS 的驱动程序。 以下是几种常见用法的**驱动程序**基于 DBMS 的驱动程序的关键字：  
  
-   **不创建数据源。** 例如，自定义应用程序可能使用一个特定的驱动程序和数据库。 如果驱动程序名称和连接到数据库所需的所有信息是硬编码在应用程序中，用户不必在其计算机运行该应用程序上创建数据源。 他们必须执行的只是安装的应用程序和驱动程序。  
  
     此方法的缺点是应用程序必须重新编译并重新分发如果连接信息发生更改。 如果数据源名称是硬编码而不是完整的连接信息的应用程序中，每个用户必须更改数据源中的信息。  
  
-   **访问特定 DBMS 一次。** 例如，通过调用 ODBC 函数中检索数据的电子表格可能包含**驱动程序**关键字来标识特定的驱动程序。 驱动程序名称为到该驱动程序的任何用户有意义，因为无法在这些用户之间传递电子表格。 如果电子表格包含数据源名称，每个用户将必须创建相同的数据源，以使用电子表格。  
  
-   **浏览到特定的驱动程序可访问的所有数据库的系统。** 有关详细信息，请参阅[使用 SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)，本部分中更高版本。
