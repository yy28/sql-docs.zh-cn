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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b10aafad95463f56ec0f5a029eac59a02cff003b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303368"
---
# <a name="choosing-a-data-source-or-driver"></a>选择数据源或驱动程序
应用程序中有时会对应用程序使用的数据源或驱动程序进行硬编码。 例如，MIS 部门编写的用于将数据从一个数据源传输到另一个数据源的自定义应用程序将包含这些数据源的名称-该应用程序将不能与任何其他数据源一起使用。 另一个示例是垂直应用程序，如用于订单输入的应用程序。 此类应用程序始终使用同一数据源，该数据源具有应用程序已知的预定义架构。  
  
 其他应用程序在运行时选择数据源或驱动程序。 通常，这些是执行即席查询的泛型应用程序，如使用 ODBC 导入数据的电子表格。 此类应用程序通常列出可用的数据源或驱动程序，并让用户选择他们想要使用的数据源或驱动程序。 一般应用程序是列出数据源、驱动程序还是同时列出它们都取决于应用程序使用的是基于 DBMS 还是基于文件的驱动程序。  
  
 基于 DBMS 的驱动程序通常需要一组复杂的连接信息，如网络地址、网络协议、数据库名称，等等。 数据源的用途是隐藏所有这些信息。 因此，数据源范例适合与基于 DBMS 的驱动程序一起使用。 应用程序可以通过以下两种方式之一向用户显示数据源列表。 它可以用**DSN** （数据源名称）关键字和无关联值调用**SQLDriverConnect** ;驱动程序管理器将显示数据源名称的列表。 如果应用程序要控制列表的外观，则它会调用**SQLDataSources**来检索可用数据源的列表，并构造自己的对话框。 此函数由驱动程序管理器实现，并且可在加载任何驱动程序之前调用。 然后，应用程序调用连接函数并向其传递所选数据源的名称。  
  
 如果未指定数据源，则使用系统信息指示的默认数据源。 （有关详细信息，请参阅[默认子项](../../../odbc/reference/install/default-subkey.md)。）如果通过使用找不到的*ServerName*参数调用**SQLConnect** ，则为 null 指针，或为 "Default"，驱动程序管理器将连接到默认数据源。 如果在对**SQLDriverConnect**或**SQLBrowseConnect**的调用中使用的连接字符串包含设置为 "default" 的**DSN**关键字，或者如果找不到指定的数据源，也会使用默认数据源。 此外，如果在对**SQLDriverConnect**的调用中使用的连接字符串不包含**DSN**关键字，则使用默认数据源。  
  
 对于基于文件的驱动程序，可以使用文件范例。 对于存储在本地计算机上的数据，用户经常知道其数据位于特定文件中，如 .dbf。 此类用户可以更轻松地选择他们知道的文件，而不是选择未知数据源。 为实现此要求，应用程序首先调用**SQLDrivers**。 此函数由驱动程序管理器实现，并且可在加载任何驱动程序之前调用。 **SQLDrivers**返回可用驱动程序的列表;它还返回**FileUsage**和**FileExtns**关键字的值。 **FileUsage**关键字说明了基于文件的驱动程序是将文件视为表（无论是 Xbase 还是数据库），因为 Microsoft®访问。 **FileExtns**关键字列出驱动程序识别的文件扩展名，例如 Xbase 驱动程序的 .dbf。 使用此信息，应用程序将构造一个对话框，用户可以通过该对话框选择文件。 然后，应用程序会根据所选文件的扩展名，使用**driver**关键字调用**SQLDriverConnect**来连接到该驱动程序。  
  
 不会阻止应用程序将数据源与基于文件的驱动程序一起使用，也无需使用**driver**关键字调用**SQLDriverConnect**来连接到基于 DBMS 的驱动程序。 下面是基于 DBMS 的驱动**程序的 DRIVER**关键字的几个常见用法：  
  
-   **不创建数据源。** 例如，自定义应用程序可能会使用特定的驱动程序和数据库。 如果在应用程序中对连接到数据库所需的驱动程序名称和所有信息进行了硬编码，则用户无需在其计算机上创建数据源即可运行该应用程序。 它们的所有操作都必须安装应用程序和驱动程序。  
  
     此方法的缺点是，如果连接信息发生更改，则必须重新编译并重新分发应用程序。 如果应用程序中的数据源名称是硬编码的，而不是完整的连接信息，则每个用户必须仅更改数据源中的信息。  
  
-   **单个时间访问特定 DBMS。** 例如，通过调用 ODBC 函数检索数据的电子表格可能包含用于识别特定驱动程序的**driver**关键字。 由于驱动程序名称对具有该驱动程序的任何用户都是有意义的，因此可以在这些用户之间传递此电子表格。 如果电子表格包含数据源名称，则每个用户都必须创建相同的数据源以使用电子表格。  
  
-   **浏览系统，查找特定驱动程序可访问的所有数据库。** 有关详细信息，请参阅本部分后面的[连接 SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。
