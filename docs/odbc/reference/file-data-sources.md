---
title: "文件数据源 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4ddd3e0db3987ed14984a978c88befbd076562b5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="file-data-sources"></a>文件数据源
*文件数据源*存储在文件中并允许重复使用单个用户或在多个用户之间共享连接信息。 当使用文件数据源时，驱动程序管理器使到使用.dsn 文件中的信息的数据源的连接。 此文件可以像任何其他文件一样操作。 文件数据源没有数据源名称，不机器数据源，以及未注册到任何一个用户或计算机。  
  
 文件数据源，从而简化了连接过程中，因为.dsn 文件包含那些原本要针对调用生成的连接字符串**SQLDriverConnect**函数。 .Dsn 文件的另一个优点是，可以将它复制到任何计算机，因此，许多计算机可以使用相同的数据源，只要它们具有适当的驱动程序。 此外可以通过应用程序共享文件数据源。 可共享的文件数据源可以放置在网络上并同时由多个应用程序。  
  
 也可以是非共享.dsn 文件。 非共享.dsn 文件位于一台计算机上，指向机数据源。 非共享的文件数据源存在主要是为了允许机器数据源轻松转换为文件数据源，以便应用程序可以设计为仅用于文件数据源。 当驱动程序管理器将信息发送非共享的文件数据源中时，连接根据需要为.dsn 文件指向机器数据源。  
  
 有关文件数据源的详细信息，请参阅[连接使用的文件数据源](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。

