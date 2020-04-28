---
title: ODBC 驱动程序体系结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 712de6a7a3f80ce1cd3ca854a88765dbfa531356
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294555"
---
# <a name="odbc-driver-architecture"></a>ODBC 驱动程序体系结构
驱动程序编写器必须知道，驱动程序体系结构可能会影响应用程序是否可以使用特定于 DBMS 的 SQL。  
  
 ![显示 ODBC 驱动程序体系结构](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [基于文件的驱动程序](../../../odbc/reference/file-based-drivers.md)  
  
 当驱动程序直接访问物理数据时，驱动程序将充当驱动程序和数据源。 驱动程序必须处理 ODBC 调用和 SQL 语句。 基于文件的驱动程序的开发人员必须编写自己的数据库引擎。  
  
 [基于 DBMS 的驱动程序](../../../odbc/reference/dbms-based-drivers.md)  
  
 当使用单独的数据库引擎来访问物理数据时，驱动程序仅处理 ODBC 调用。 它将 SQL 语句传递到数据库引擎进行处理。  
  
 [网络体系结构](../../../odbc/reference/network-example.md)  
  
 文件和 DBMS ODBC 配置可以存在于单个网络上。  
  
 [其他驱动程序体系结构](../../../odbc/reference/other-driver-architectures.md)  
  
 当需要驱动程序使用各种数据源时，可以将其用作中间件。 异类联接引擎的体系结构可以使驱动程序显示为驱动程序管理器。 还可以在服务器上安装驱动程序，它们可由一系列客户端共享。  
  
 有关驱动程序体系结构的详细信息，请参阅有关[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)的部分中的[驱动程序管理器](../../../odbc/reference/the-driver-manager.md)和[驱动程序体系结构](../../../odbc/reference/driver-architecture.md)。  
  
 有关驱动程序问题的详细信息，请参阅下表中所述的位置。  
  
|问题|主题|位置|  
|-----------|-----------|--------------|  
|应用程序和驱动程序的兼容性问题|[应用程序/驱动程序兼容性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|ODBC 程序员参考中的[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)|  
|编写 ODBC 驱动程序|[编写 ODBC 3.x 驱动程序](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|ODBC 程序员参考中的[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)|  
|向后兼容的驱动程序准则|[驱动程序后向兼容性准则](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|附录 G： ODBC 程序员参考中的[用于向后兼容的驱动程序准则](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|  
|连接到驱动程序|[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|在 ODBC 程序员参考中[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)|  
|识别驱动程序|[查看驱动程序](../../../odbc/admin/viewing-drivers.md)|查看 Microsoft ODBC 数据源管理器联机帮助中的[驱动程序](../../../odbc/admin/viewing-drivers.md)|  
|启用连接池|[ODBC 连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|在 ODBC 程序员参考中[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)|  
|Unicode/ANSI 驱动程序和连接问题|[Unicode 驱动程序](../../../odbc/reference/develop-app/unicode-drivers.md)|ODBC 程序员参考中的[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)|  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
