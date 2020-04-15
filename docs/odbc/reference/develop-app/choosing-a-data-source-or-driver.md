---
title: 选择数据源或驱动程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b10aafad95463f56ec0f5a029eac59a02cff003b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303368"
---
# <a name="choosing-a-data-source-or-driver"></a>选择数据源或驱动程序
应用程序使用的数据源或驱动程序有时在应用程序中是硬编码的。 例如，MIS 部门编写的将数据从一个数据源传输到另一个数据源的自定义应用程序将包含这些数据源的名称-该应用程序根本不适用于任何其他数据源。 另一个示例是垂直应用程序，例如用于订单输入的应用程序。 此类应用程序始终使用相同的数据源，该数据源具有应用程序已知的预定义架构。  
  
 其他应用程序在运行时选择数据源或驱动程序。 通常，这些是执行临时查询的通用应用程序，例如使用 ODBC 导入数据的电子表格。 此类应用程序通常列出可用的数据源或驱动程序，并允许用户选择要使用的数据源或驱动程序。 通用应用程序是否经常列出数据源、驱动程序或两者，取决于应用程序是使用基于 DBMS 还是基于文件的驱动程序。  
  
 基于 DBMS 的驱动程序通常需要一组复杂的连接信息，例如网络地址、网络协议、数据库名称等。 数据源的目的是隐藏所有这些信息。 因此，数据源范例可用于基于 DBMS 的驱动程序。 应用程序可以通过以下两种方式之一向用户显示数据源列表。 它可以使用**DSN（** 数据源名称）关键字调用**SQLDriverConnect，** 并且没有关联的值;驱动程序管理器将显示数据源名称的列表。 如果应用程序希望控制列表的外观，它将调用**SQLDataSources**来检索可用数据源的列表并构造其自己的对话框。 此功能由驱动程序管理器实现，可以在加载任何驱动程序之前调用。 然后，应用程序调用连接函数并传递所选数据源的名称。  
  
 如果未指定数据源，则使用系统信息指示的默认数据源。 （有关详细信息，请参阅[默认子键](../../../odbc/reference/install/default-subkey.md)。如果使用找不到的*服务器Name*参数、空指针或"DEFAULT"调用**SQLConnect，** 则驱动程序管理器将连接到默认数据源。 如果调用**SQLDriverConnect**或**SQLBrowseConnect**中使用的连接字符串包含设置为"DEFAULT"的**DSN**关键字，或者找不到指定的数据源，则还会使用默认数据源。 此外，如果调用**SQLDriverConnect**中使用的连接字符串不包含**DSN**关键字，则使用默认数据源。  
  
 使用基于文件的驱动程序，可以使用文件范例。 对于存储在本地计算机上的数据，用户经常知道他们的数据位于特定文件中，如 Employ.dbf。 此类用户可以更轻松地选择他们知道的文件，而不是选择未知的数据源。 为了实现这一点，应用程序首先调用**SQLDrivers**。 此功能由驱动程序管理器实现，可以在加载任何驱动程序之前调用。 **SQLDrivers**返回可用驱动程序的列表;它还返回**文件使用情况**和**文件Extn**关键字的值。 **FileUsage**关键字解释基于文件的驱动程序是像 Xbase 一样将文件视为表，还是将文件视为数据库，Microsoft®访问也是如此。 **FileExtns**关键字列出了驱动程序识别的文件名扩展名，例如 Xbase 驱动程序的 .dbf。 使用此信息，应用程序将构造一个对话框，用户通过该对话框选择文件。 根据所选文件的扩展名，应用程序然后通过使用 DRIVER 关键字调用**SQLDriverConnect**连接到**驱动程序**。  
  
 没有什么可以阻止应用程序使用具有基于文件的驱动程序的数据源，或者使用**DRIVER**关键字调用**SQLDriverConnect**以连接到基于 DBMS 的驱动程序。 以下是基于 DBMS 的**驱动程序**的 DRIVER 关键字的几个常见用途：  
  
-   **不创建数据源。** 例如，自定义应用程序可能使用特定的驱动程序和数据库。 如果驱动程序名称和连接到数据库所需的所有信息在应用程序中是硬编码的，则用户不必在其计算机上创建数据源即可运行应用程序。 他们必须做的是安装应用程序和驱动程序。  
  
     此方法的缺点是，如果连接信息发生更改，则必须重新编译和重新分发应用程序。 如果在应用程序中硬编码数据源名称，而不是完整的连接信息，则每个用户必须仅更改数据源中的信息。  
  
-   **一次访问特定的 DBMS。** 例如，通过调用 ODBC 函数检索数据的电子表格可能包含用于标识特定驱动程序的**DRIVER**关键字。 由于驱动程序名称对于任何具有该驱动程序的用户都有意义，因此可以在这些用户之间传递电子表格。 如果电子表格包含数据源名称，则每个用户必须创建相同的数据源才能使用电子表格。  
  
-   **浏览特定驱动程序可访问的所有数据库的系统。** 有关详细信息，请参阅本节后面的[SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。
