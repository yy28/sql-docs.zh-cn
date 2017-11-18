---
title: "数据源向导屏幕 2 (ODBC Driver for SQL Server) |Microsoft 文档"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e861bc52621e520a27e930dd22f1a1eb9613cc76
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="data-source-wizard-screen-2"></a>数据源向导屏幕 2

指定的方法的身份验证，并设置 Microsoft SQL Server 高级客户端条目的登录名和密码的 ODBC driver for SQL Server 将使用配置数据源时连接到 SQL Server。

## <a name="options"></a>选项

### <a name="with-integrated-windows-authentication"></a>使用集成的 Windows 身份验证

指定驱动程序请求到的 SQL Server 的安全 （或受信任） 连接。 选中后，SQL Server 将使用集成登录安全性来建立使用此数据源的连接，而不考虑服务器上的当前登录安全模式。 提供的任何登录 ID 或密码都将忽略。 SQL Server 系统管理员必须有关联的 Windows 登录名与 SQL Server 登录 ID （例如，通过使用 SQL Server Management Studio）。

您还可以指定该服务器的服务主体名称 (SPN)。

### <a name="with-active-directory-integrated-authentication"></a>与 Active Directory 集成的身份验证

指定驱动程序向 SQL Server 使用 Azure Active Directory 进行身份验证。 当选中时，SQL Server 将使用 Azure Active Directory 集成的登录安全性来建立连接使用此数据源，而不考虑服务器上当前的登录安全模式。

### <a name="with-sql-server-authentication"></a>使用 SQL Server 身份验证

指定驱动程序向 SQL Server 使用的登录 ID 和密码进行身份验证。

### <a name="with-active-directory-password-authentication"></a>使用 Active Directory 密码身份验证

指定驱动程序向 SQL Server 使用 Azure Active Directory 登录 ID 和密码进行身份验证。

### <a name="login-id"></a>登录 ID

指定如果连接到 SQL Server 时，将使用该驱动程序的登录 ID**与 SQL Server 身份验证使用的登录 ID 和用户输入的密码**或**使用登录 ID 与 Active Directory 密码身份验证和用户输入的密码**选择。 这仅适用于为确定服务器默认设置建立的连接；不适用于创建数据源之后使用该数据源建立的后续连接。

### <a name="password"></a>密码

指定如果连接到 SQL Server 时，将使用该驱动程序的密码**与 SQL Server 身份验证使用的登录 ID 和用户输入的密码**或**使用登录 ID 与 Active Directory 密码身份验证和用户输入的密码**选择。 这仅适用于为确定服务器默认设置建立的连接；不适用于使用新数据源建立的后续连接。

这两个**登录 ID**和**密码**如果禁用了框**使用集成 Windows 身份验证**或**与 Active Directory 集成身份验证**选择。

### <a name="next"></a>Next

转到向导的下一个屏幕。

### <a name="back"></a>返回

返回到向导的上一屏幕。

## <a name="next-steps"></a>后续步骤

[数据源向导屏幕 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[数据源向导屏幕 3](../../../connect/odbc/windows/dsn-wizard-3.md)


