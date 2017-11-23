---
title: "ODBC 驱动程序体系结构 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ecde72ec7bd66fa3cc52ae70a3ca626ada2c0818
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-driver-architecture"></a>ODBC 驱动程序体系结构
驱动程序编写器必须注意驱动程序体系结构可能会影响是否应用程序可以使用特定于 DBMS 的 SQL。  
  
 ![显示的 ODBC 驱动程序体系结构](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [基于文件的驱动程序](../../../odbc/reference/file-based-drivers.md)  
  
 当该驱动程序直接访问物理数据时，该驱动程序充当驱动程序和数据源。 该驱动程序必须处理 ODBC 调用和 SQL 语句。 基于文件的驱动程序的开发人员必须编写自己的数据库引擎。  
  
 [基于 DBMS 的驱动程序](../../../odbc/reference/dbms-based-drivers.md)  
  
 当单独的数据库引擎用于访问物理数据时，该驱动程序将处理仅 ODBC 调用。 它将传递 SQL 语句对数据库引擎处理。  
  
 [网络体系结构](../../../odbc/reference/network-example.md)  
  
 文件和 DBMS ODBC 配置可以存在于单一网络。  
  
 [其他驱动程序体系结构](../../../odbc/reference/other-driver-architectures.md)  
  
 当需要驱动程序时要使用不同的数据源时，则它可以用中间件。 异类联接引擎体系结构可以显示为驱动程序管理器的驱动程序。 也可以在其中它们可以由一系列的客户端共享的服务器上安装驱动程序。  
  
 有关驱动程序体系结构的详细信息，请参阅[驱动程序管理器](../../../odbc/reference/the-driver-manager.md)和[驱动程序体系结构](../../../odbc/reference/driver-architecture.md)上的部分[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)。  
  
 可以在下表中描述的位置中找到有关驱动程序问题的详细信息。  
  
|问题|主题|位置|  
|-----------|-----------|--------------|  
|与应用程序和驱动程序兼容性问题|[应用程序/驱动程序兼容性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)，ODBC 程序员参考中|  
|编写 ODBC 驱动程序|[编写 ODBC 3.x 驱动程序](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)，ODBC 程序员参考中|  
|为了向后兼容的驱动程序准则|[为了向后兼容的驱动程序准则](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[附录 g： 为了向后兼容驱动程序准则](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)，ODBC 程序员参考中|  
|连接到驱动程序|[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)，ODBC 程序员参考中|  
|标识驱动程序|[查看驱动程序](../../../odbc/admin/viewing-drivers.md)|[查看驱动程序](../../../odbc/admin/viewing-drivers.md)中的 Microsoft ODBC 数据源管理器的联机帮助|  
|启用连接池|[ODBC 连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)，ODBC 程序员参考中|  
|Unicode/ANSI 驱动程序和连接问题|[Unicode 驱动程序](../../../odbc/reference/develop-app/unicode-drivers.md)|[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)，ODBC 程序员参考中|  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
