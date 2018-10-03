---
title: 选择数据源或驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e47248ac5719b2303c71f2e7b93161112ca7f870
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758035"
---
# <a name="choosing-a-data-source-or-driver"></a>选择数据源或驱动程序
数据源或驱动程序使用的应用程序有时是硬编码应用程序中。 例如，编写由 MIS 部门将传输到另一个数据源中的数据将包含这些数据源的名称的自定义应用程序 — 应用程序只需将不起作用的任何其他数据源。 另一个示例是垂直的应用程序，例如一个用于订单条目。 此类应用程序始终使用相同数据源，该源具有已知的应用程序的预定义的架构。  
  
 其他应用程序在运行时选择的数据源或驱动程序。 通常情况下，它们是执行即席查询，如使用 ODBC 将数据导入电子表格的泛型应用程序。 通常，此类应用程序列出可用的数据源或驱动程序，并使用户可以选择他们的想要使用。 是否通用应用程序列出数据源、 驱动程序，或两者通常取决于应用程序是否使用基于 DBMS 的或基于文件的驱动程序。  
  
 基于 DBMS 的驱动程序通常需要一组复杂的连接信息，如网络地址、 网络协议、 数据库名称和等等。 数据源的目的是隐藏所有这些信息。 因此，数据源模式适合用于基于 DBMS 的驱动程序。 应用程序可在两种方式之一向用户显示数据源的列表。 它可以调用**SQLDriverConnect**与**DSN** （数据源名称） 关键字和任何关联的值; 驱动程序管理器将显示数据源名称的列表。 如果应用程序希望控制列表的外观，则会调用**SQLDataSources**要检索的一组可用数据源，构造其自有对话框。 此函数实现由驱动程序管理器，并可加载的任何驱动程序之前调用。 然后，应用程序调用连接函数，并将其传递所选的数据源的名称。  
  
 如果未指定数据源，则使用系统信息中指明的默认数据源。 (有关详细信息，请参阅[默认子项](../../../odbc/reference/install/default-subkey.md)。)如果**SQLConnect**通过使用调用*ServerName*找不到、 为 null 指针，或为"DEFAULT"的参数，驱动程序管理器连接到默认数据源。 对的调用中使用的连接字符串，也将使用数据源的默认**SQLDriverConnect**或**SQLBrowseConnect**包含**DSN**关键字设置为"默认值"或者如果找不到指定的数据源。 此外，对的调用中使用的连接字符串，如果使用数据源，则默认值**SQLDriverConnect**不包含**DSN**关键字。  
  
 基于文件的驱动程序后，就可以使用一种文件的模式。 对于存储在本地计算机上的数据，用户通常知道他们的数据是在特定文件，如 Employee.dbf。 而不是选择未知的数据源，是此类用户选择他们知道的文件更容易。 若要实现此操作，应用程序首先调用**SQLDrivers**。 此函数实现由驱动程序管理器，并可加载的任何驱动程序之前调用。 **SQLDrivers**返回一系列可用的驱动程序; 它还会返回值**FileUsage**并**FileExtns**关键字。 **FileUsage**关键字说明是否基于文件的驱动程序将文件视为表，不 Xbase，或作为数据库，作为执行 Microsoft® 访问。 **FileExtns**关键字列出了可以识别驱动程序，如 Xbase 驱动程序的.dbf 文件扩展名。 使用此信息，应用程序会构造一个对话框，通过该用户选择一个文件。 根据所选文件的扩展名，然后，应用程序连接到该驱动程序通过调用**SQLDriverConnect**与**驱动程序**关键字。  
  
 没有要停止从数据源中使用基于文件的驱动程序或调用应用程序**SQLDriverConnect**与**驱动程序**关键字来连接到基于 DBMS 的驱动程序。 以下是几个常见的用法**驱动程序**基于 DBMS 的驱动程序的关键字：  
  
-   **不创建数据源。** 例如，自定义应用程序可能会使用特定的驱动程序和数据库。 如果驱动程序名称和连接到数据库所需的所有信息是硬编码应用程序中，用户不必自己运行该应用程序的计算机上创建数据源。 它们必须做的是安装的应用程序和驱动程序。  
  
     此方法的缺点是必须重新编译和重新分发的连接信息更改应用程序。 如果数据源名称是硬编码而不是完整的连接信息在应用程序中，每个用户必须更改仅在数据源中的信息。  
  
-   **访问特定 DBMS 一次。** 例如，可能包含通过调用 ODBC 函数检索数据的电子表格**驱动程序**关键字来标识特定的驱动程序。 驱动程序名称是对任何具有该驱动程序的用户有意义，因为无法在这些用户之间传递该电子表格。 如果该电子表格包含数据源名称，每个用户需要创建相同的数据源，以使用电子表格。  
  
-   **浏览到特定的驱动程序可访问的所有数据库的系统。** 有关详细信息，请参阅[使用 SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)，在本部分中更高版本。
