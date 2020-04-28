---
title: 文件数据源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0661aa424a7a118b8b12f4bf8433987ff83bd788
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306648"
---
# <a name="file-data-sources"></a>文件数据源
*文件数据源*存储在文件中，并允许单个用户重复使用连接信息或在多个用户之间共享连接信息。 使用文件数据源时，驱动程序管理器使用 .dsn 文件中的信息与数据源建立连接。 此文件可以像任何其他文件一样操作。 文件数据源没有数据源名称（与计算机数据源相同），并且未注册到任何一个用户或计算机。  
  
 文件数据源可简化连接过程，因为 .dsn 文件包含连接字符串，否则必须为**SQLDriverConnect**函数的调用生成该字符串。 .Dsn 文件的另一个优点是可以将其复制到任何计算机上，因此，许多计算机可以使用相同的数据源，只要它们安装了适当的驱动程序即可。 文件数据源还可以由应用程序共享。 可共享的文件数据源可以放置在网络上并可由多个应用程序同时使用。  
  
 .Dsn 文件也可以是 unshareable。 Unshareable 文件位于单台计算机上，指向计算机数据源。 Unshareable 文件数据源的存在主要是为了使计算机数据源轻松地转换为文件数据源，以便可以将应用程序设计为仅使用文件数据源。 当驱动程序管理器发送 unshareable 文件数据源中的信息时，它会根据需要连接到该 .dsn 文件所指向的计算机数据源。  
  
 有关文件数据源的详细信息，请参阅[使用文件数据源进行连接或使用](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。
