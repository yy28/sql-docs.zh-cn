---
title: 用于 Oracle 的 ODBC 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 093cb7352a7f509b0afcc061e2691311bb183169
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298127"
---
# <a name="odbc-driver-for-oracle"></a>Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 Microsoft® ODBC Driver for Oracle 允许您将与 ODBC 兼容的应用程序连接到 Oracle 数据库。 用于 Oracle 的 ODBC 驱动程序符合*Odbc 程序员参考*中介绍的开放式数据库连接（odbc）规范。 它允许从 Internet Information Services （IIS）内访问 PL/SQL 包、XA/DTC 集成和 Oracle 访问。  
  
 Oracle RDBMS 是使用各种工作站和 minicomputer 操作系统运行的多用户关系数据库管理系统。 运行 Microsoft Windows 的 IBM 兼容计算机可以通过网络与 Oracle 数据库服务器通信。 支持的网络包括 Microsoft LAN Manager、NetWare、VINES、DECnet 和支持 TCP/IP 的任何网络。  
  
 通过用于 Oracle 的 ODBC 驱动程序，应用程序可以通过 ODBC 接口访问 Oracle 数据库中的数据。 该驱动程序可以访问本地 Oracle 数据库，也可以通过 SQL * Net 与网络通信。 下图详细说明了此应用程序和驱动程序体系结构。  
  
 ![用于 Oracle 应用&#47;驱动程序体系结构的 ODBC 驱动程序](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 用于 Oracle 的 ODBC 驱动程序符合 API 一致性级别1和 SQL 一致性级别核心。 它还支持 API 一致性级别2中的某些函数，以及核心和扩展 SQL 一致性级别中的大部分语法。 驱动程序符合 ODBC 2.5，并支持32位系统。 Oracle 7.3 x 完全受支持;Oracle8 提供有限的支持。 用于 Oracle 的 ODBC 驱动程序不支持任何新的 Oracle8 数据类型（Unicode 数据类型、Blob、Clob 等），也不支持 Oracle 的新关系对象模型。 有关支持的数据类型的详细信息，请参阅本指南中[支持的数据类型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)。  
  
 若要访问 Oracle 数据，需要以下组件：  
  
-   用于 Oracle 的 ODBC 驱动程序  
  
-   Oracle RDBMS 数据库  
  
-   Oracle 客户端软件  
  
 此外，对于远程连接：  
  
-   连接运行驱动程序和数据库的计算机的网络。 网络必须支持 SQL * 网络连接。  
  
## <a name="component-documentation"></a>组件文档  
 本指南包含有关设置和配置用于 Oracle 的 Microsoft ODBC 驱动程序并添加编程功能的详细信息。 它还包含技术参考资料。  
  
 有关特定 Oracle 产品行为的信息，请参阅 Oracle 产品附带的文档。  
  
 有关使用 ODBC 数据源管理器设置或配置用于 Oracle 的 Microsoft ODBC 驱动程序的信息，请参阅[Odbc 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)文档。  
  
 本部分包含以下主题。  
  
-   [Oracle ODBC 驱动程序用户指南](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Oracle ODBC 驱动程序程序员参考](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
