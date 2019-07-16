---
title: Oracle ODBC 驱动程序 |Microsoft Docs
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
ms.openlocfilehash: 8fc15968501fed6b94a7ccddb984cbdf76bcbcb0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915807"
---
# <a name="odbc-driver-for-oracle"></a>Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 适用于 Oracle 的 Microsoft® ODBC 驱动程序，可在符合 ODBC 的应用程序连接到 Oracle 数据库。 Oracle ODBC 驱动程序符合开放式数据库连接 (ODBC) 规范中所述*ODBC 程序员参考*。 它允许访问 PL/SQL 包、 XA/DTC 集成和 Oracle 访问从 Internet 信息服务 (IIS) 中。  
  
 Oracle RDBMS 是与各种工作站和小型计算机的操作系统运行的多用户关系数据库管理系统。 运行 Microsoft Windows 的 IBM 兼容计算机可以通过网络与 Oracle 数据库服务器通信。 受支持的网络包括 Microsoft LAN 管理器、 NetWare、 VINES、 DECnet 和支持 TCP/IP 的任何网络。  
  
 Oracle ODBC 驱动程序使应用程序能够通过 ODBC 接口访问 Oracle 数据库中的数据。 该驱动程序可以访问本地 Oracle 数据库或其能够与通过 SQL 网络通信 * Net。 下图详细介绍了此应用程序和驱动程序体系结构。  
  
 ![Oracle 应用程序的 ODBC 驱动程序&#47;驱动程序体系结构](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Oracle ODBC 驱动程序符合 API 一致性级别 1 和 SQL 一致性级别核心。 它还支持 API 的一致性级别 2 和大部分核心应用程序和扩展 SQL 一致性级别中的语法中的某些函数。 驱动程序符合 ODBC 2.5，支持 32 位系统。 Oracle 7.3 x 支持完全;Oracle8 受到有限的支持。 Oracle ODBC 驱动程序不支持的任何新 Oracle8 数据类型的 Unicode 数据类型、 Blob、 Clob 和等等的也不支持 Oracle 的新的关系对象模型。 有关支持的数据类型的详细信息，请参阅[支持的数据类型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)本指南中。  
  
 若要访问 Oracle 数据，都需要以下组件：  
  
-   Oracle ODBC 驱动程序  
  
-   Oracle RDBMS 数据库  
  
-   Oracle 客户端软件  
  
 此外，对于远程连接：  
  
-   运行该驱动程序和数据库的计算机连接网络。 网络必须支持的 SQL * Net 连接。  
  
## <a name="component-documentation"></a>组件文档  
 本指南包含有关设置和配置适用于 Oracle 的 Microsoft ODBC 驱动程序和添加编程功能的详细的信息。 它还包含技术参考材料。  
  
 有关特定的 Oracle 产品行为的信息，请参阅随附的 Oracle 产品的文档。  
  
 有关设置或配置 Microsoft ODBC Driver for Oracle 使用 ODBC 数据源管理器的信息，请参阅[ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)文档。  
  
 本部分包含以下主题。  
  
-   [Oracle ODBC 驱动程序用户指南](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Oracle ODBC 驱动程序程序员参考](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
