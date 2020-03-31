---
title: 甲骨文的ODBC驱动程序 |微软文档
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b5f1aabd23a587e681c33aed4b4119523444219
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402615"
---
# <a name="odbc-driver-for-oracle"></a>Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用[Oracle 提供的 ODBC 驱动程序](https://www.oracle.com/database/technologies/releasenote-odbc-ic.html)。  
  
 Microsoft® Oracle 的 ODBC 驱动程序允许您将符合 ODBC 的应用程序连接到 Oracle 数据库。 Oracle 的 ODBC 驱动程序符合*ODBC 程序员参考*中所述的开放数据库连接 （ODBC） 规范。 它允许从 Internet 信息服务 （IIS） 访问 PL/SQL 包、XA/DTC 集成和 Oracle 访问。  
  
 Oracle RDBMS 是一个多用户关系数据库管理系统，可运行各种工作站和微型计算机操作系统。 运行 Microsoft Windows 的 IBM 兼容计算机可以通过网络与 Oracle 数据库服务器进行通信。 支持的网络包括微软局域网管理器、网华、VINES、DECnet 以及任何支持 TCP/IP 的网络。  
  
 Oracle 的 ODBC 驱动程序使应用程序能够通过 ODBC 接口访问 Oracle 数据库中的数据。 驱动程序可以访问本地 Oracle 数据库，也可以通过 SQL_Net 与网络通信。 下图详细介绍了此应用程序和驱动程序体系结构。  
  
 ![用于 Oracle 应用的 ODBC 驱动程序&#47;驱动程序体系结构](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Oracle 的 ODBC 驱动程序符合 API 符合级别 1 和 SQL 一致性级别核心。 它还支持 API 一致性级别 2 中的某些函数以及核心和扩展 SQL 一致性级别中的大部分语法。 该驱动程序符合 ODBC 2.5 标准，支持 32 位系统。 完全支持 Oracle 7.3x;Oracle8 的支持有限。 Oracle 的 ODBC 驱动程序不支持任何新的 Oracle8 数据类型 - Unicode 数据类型、BB、CLOB 等 ， 也不支持 Oracle 新的关系对象模型。 有关支持的数据类型的详细信息，请参阅本指南中[支持的类型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)。  
  
 要访问 Oracle 数据，需要以下组件：  
  
-   甲骨文的ODBC驱动程序  
  
-   甲骨文RDBMS数据库  
  
-   甲骨文客户端软件  
  
 此外，对于远程连接：  
  
-   连接运行驱动程序和数据库的计算机的网络。 网络必须支持 SQL_Net 连接。  
  
## <a name="component-documentation"></a>组件文档  
 本指南包含有关为 Oracle 设置和配置 Microsoft ODBC 驱动程序以及添加编程功能的详细信息。 它还包含技术参考材料。  
  
 有关特定 Oracle 产品行为的信息，请参阅随 Oracle 产品随附的文档。  
  
 有关使用 ODBC 数据源管理员为 Oracle 设置或配置 Microsoft ODBC 驱动程序的信息，请参阅[ODBC 数据源管理员](../../odbc/admin/odbc-data-source-administrator.md)文档。  
  
 本部分包含以下主题。  
  
-   [Oracle ODBC 驱动程序用户指南](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Oracle ODBC 驱动程序程序员参考](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
