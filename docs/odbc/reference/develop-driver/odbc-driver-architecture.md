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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d123bdf1ea3357a4846a223c41950c952c1af2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915537"
---
# <a name="odbc-driver-architecture"></a>ODBC 驱动程序体系结构
驱动程序编写人员必须了解驱动程序体系结构可能会影响是否应用程序可以使用特定于 DBMS 的 SQL。  
  
 ![显示 ODBC 驱动程序体系结构](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [基于文件的驱动程序](../../../odbc/reference/file-based-drivers.md)  
  
 当驱动程序直接访问物理数据时，该驱动程序充当驱动程序和数据源。 该驱动程序必须处理 ODBC 调用和 SQL 语句。 基于文件的驱动程序的开发人员必须编写自己的数据库引擎。  
  
 [基于 DBMS 的驱动程序](../../../odbc/reference/dbms-based-drivers.md)  
  
 在单独的数据库引擎用于访问物理数据，该驱动程序处理仅 ODBC 调用。 它将 SQL 语句传递到数据库引擎处理。  
  
 [网络体系结构](../../../odbc/reference/network-example.md)  
  
 文件和 DBMS ODBC 配置可以在单个网络上存在。  
  
 [其他驱动程序体系结构](../../../odbc/reference/other-driver-architectures.md)  
  
 如果驱动程序需要来使用不同的数据源，它可以用作中间件。 异类联接引擎体系结构可以使显示驱动程序管理器为驱动程序。 此外可以在其中它们可以由一系列的客户端共享的服务器上安装驱动程序。  
  
 有关驱动程序体系结构的详细信息，请参阅[驱动程序管理器](../../../odbc/reference/the-driver-manager.md)并[驱动程序体系结构](../../../odbc/reference/driver-architecture.md)上的部分中[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)。  
  
 可以在下表中描述的位置中找到有关驱动程序问题的详细信息。  
  
|问题|主题|Location|  
|-----------|-----------|--------------|  
|与应用程序和驱动程序兼容性问题|[应用程序/驱动程序兼容性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)中的 ODBC 程序员参考|  
|编写 ODBC 驱动程序|[编写 ODBC 3.x 驱动程序](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)中的 ODBC 程序员参考|  
|为了向后兼容的驱动程序指南|[为了向后兼容的驱动程序指南](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[附录 g:为了向后兼容的驱动程序指南](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)中的 ODBC 程序员参考|  
|连接到驱动程序|[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)中的 ODBC 程序员参考|  
|识别驱动程序|[查看驱动程序](../../../odbc/admin/viewing-drivers.md)|[查看驱动程序](../../../odbc/admin/viewing-drivers.md)中的 Microsoft ODBC 数据源管理器联机帮助|  
|启用连接池|[ODBC 连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)中的 ODBC 程序员参考|  
|Unicode/ANSI 驱动程序和连接问题|[Unicode 驱动程序](../../../odbc/reference/develop-app/unicode-drivers.md)|[编程注意事项](../../../odbc/reference/develop-app/programming-considerations.md)中的 ODBC 程序员参考|  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
