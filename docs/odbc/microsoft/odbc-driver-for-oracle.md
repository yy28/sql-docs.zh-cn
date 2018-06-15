---
title: 适用于 Oracle 的 ODBC 驱动程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a129bbc39f35c2418fc0dc5d34e534d4c7fb8cbc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902242"
---
# <a name="odbc-driver-for-oracle"></a>适用于 Oracle 的 ODBC 驱动程序
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 适用于 Oracle 的 Microsoft® ODBC 驱动程序允许你连接到 Oracle 数据库符合 ODBC 的应用程序。 用于 Oracle 的 ODBC 驱动程序符合开放式数据库连接 (ODBC) 规范中所述*ODBC 程序员参考*。 它允许访问 PL/SQL 包、 XA/DTC 集成和 Oracle 访问从在 Internet 信息服务 (IIS)。  
  
 Oracle RDBMS 是与各种工作站和小型计算机的操作系统运行的多用户的关系数据库管理系统。 运行 Microsoft Windows 的 IBM 兼容计算机可以在通过网络与 Oracle 数据库服务器通信。 支持的网络包括 Microsoft LAN 管理器、 NetWare、 VINES、 DECnet 和支持 TCP/IP 任何网络。  
  
 用于 Oracle 的 ODBC 驱动程序可让应用程序通过 ODBC 界面访问 Oracle 数据库中的数据。 驱动程序可以访问本地 Oracle 数据库或其能够与通过 SQL 网络通信 * Net。 下图详细说明了此应用程序和驱动程序的体系结构。  
  
 ![ODBC Driver for Oracle 应用&#47;驱动程序体系结构](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 用于 Oracle 的 ODBC 驱动程序遵守 API 一致性级别 1 和 SQL 一致性级别核心。 它还支持 API 一致性级别 2 和大部分核心和扩展 SQL 一致性级别中的语法中的某些函数。 该驱动程序 ODBC 2.5 符合并支持 32 位系统。 Oracle 7.3 x 支持完全;Oracle8 提供有限支持。 用于 Oracle 的 ODBC 驱动程序不支持的任何新 Oracle8 数据类型，Unicode 数据类型，Blob、 Clob，，依此类推 — 也不支持 Oracle 的新的关系对象模型。 有关支持的数据类型的详细信息，请参阅[支持的数据类型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)本指南中。  
  
 若要访问 Oracle 数据，都需要以下组件：  
  
-   用于 Oracle 的 ODBC 驱动程序  
  
-   Oracle RDBMS 数据库  
  
-   Oracle 客户端软件  
  
 此外，为远程连接：  
  
-   运行该驱动程序和数据库的计算机连接网络。 网络必须支持 SQL * Net 连接。  
  
## <a name="component-documentation"></a>组件文档  
 本指南包含有关设置和配置 Microsoft ODBC Driver for Oracle 和添加编程功能的详细的信息。 它还包含技术参考材料。  
  
 有关特定的 Oracle 产品行为的信息，请查阅随附 Oracle 产品的文档。  
  
 有关设置或配置 Microsoft ODBC Driver for Oracle 使用 ODBC 数据源管理器的信息，请参阅[ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)文档。  
  
 本部分包含以下主题。  
  
-   [Oracle ODBC 驱动程序用户指南](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Oracle ODBC 驱动程序程序员参考](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
