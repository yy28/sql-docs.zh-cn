---
title: 数据源向导屏幕 2 （适用于 SQL Server ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
manager: craigg
ms.openlocfilehash: 7d352b02d118c3de14cd437daf012885d7491c1b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639515"
---
# <a name="data-source-wizard-screen-2"></a>数据源向导屏幕 2

指定身份验证方法，并设置 Microsoft SQL Server 高级客户端条目，以及适用于 SQL Server 的 ODBC 驱动程序在配置数据源时用于连接到 SQL Server 的登录名和密码。

## <a name="options"></a>选项

### <a name="with-integrated-windows-authentication"></a>使用集成 Windows 身份验证

指定驱动程序请求的安全 （或可信） 连接到 SQL Server。 选中后，SQL Server 将使用集成登录安全性来建立使用此数据源的连接，而不考虑服务器上的当前登录安全模式。 提供的任何登录 ID 或密码都将忽略。 SQL Server 系统管理员必须具有关联的 Windows 登录名与 SQL Server 登录 ID （例如，通过使用 SQL Server Management Studio）。

您还可以指定该服务器的服务主体名称 (SPN)。

### <a name="with-active-directory-integrated-authentication"></a>使用 Active Directory 集成身份验证

指定驱动程序向 SQL Server 使用 Azure Active Directory 进行身份验证。 选中后，SQL Server 通过 Azure Active Directory 集成登录安全性使用此数据源来建立连接，而不考虑服务器上的当前登录安全模式。

### <a name="with-sql-server-authentication"></a>使用 SQL Server 身份验证

指定驱动程序向 SQL Server 使用的登录 ID 和密码进行身份验证。

### <a name="with-active-directory-password-authentication"></a>使用 Active Directory 密码身份验证

指定驱动程序向 SQL Server 使用的是 Azure Active Directory 登录 ID 和密码进行身份验证。

### <a name="with-active-directory-interactive-authentication"></a>使用 Active Directory 交互式身份验证

指定驱动程序向 SQL Server 通过提供登录名 id。 使用 Azure Active Directory 交互模式下进行身份验证 这会触发 Windows Azure 身份验证提示对话框。

### <a name="login-id"></a>登录 ID

指定如果连接到 SQL Server 时，驱动程序使用的登录 ID**使用 SQL Server 身份验证使用的登录 ID 和密码输入的用户名**或**与 Active Directory 密码身份验证的登录 id输入的用户和密码**或**用户输入与 Active Directory 交互式身份验证的登录 id**处于选中状态。 这仅适用于为确定服务器默认设置建立的连接；不适用于创建数据源之后使用该数据源建立的后续连接。

### <a name="password"></a>Password

指定如果连接到 SQL Server 时，驱动程序使用的密码**使用 SQL Server 身份验证使用的登录 ID 和密码输入的用户名**或**与 Active Directory 密码身份验证的登录 id输入的用户和密码**处于选中状态。 这仅适用于为确定服务器默认设置建立的连接；不适用于使用新数据源建立的后续连接。

这两个**登录 ID**并**密码**框处于禁用状态，如果**使用集成 Windows 身份验证**或**与 Active Directory 集成身份验证**处于选中状态。

### <a name="next"></a>Next

继续到向导的下一个屏幕。

### <a name="back"></a>返回

返回到向导的上一屏幕。

## <a name="next-steps"></a>后续步骤

[数据源向导屏幕 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[数据源向导屏幕 3](../../../connect/odbc/windows/dsn-wizard-3.md)

