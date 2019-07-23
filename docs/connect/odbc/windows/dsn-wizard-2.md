---
title: 数据源向导屏幕 2 (ODBC Driver for SQL Server) |Microsoft Docs
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
ms.openlocfilehash: c997dd30b6d1e9844843ff4fa626c46b42fed463
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936576"
---
# <a name="data-source-wizard-screen-2"></a>数据源向导屏幕 2

指定身份验证方法，并设置 Microsoft SQL Server 高级客户端条目，以及适用于 SQL Server 的 ODBC 驱动程序在配置数据源时用于连接到 SQL Server 的登录名和密码。

## <a name="options"></a>选项

### <a name="with-integrated-windows-authentication"></a>使用集成 Windows 身份验证

指定驱动程序请求与 SQL Server 的安全 (或可信) 连接。 选中后，SQL Server 将使用集成登录安全性来建立使用此数据源的连接，而不考虑服务器上的当前登录安全模式。 提供的任何登录 ID 或密码都将忽略。 SQL Server 系统管理员必须将您的 Windows 登录名与 SQL Server 登录 ID 相关联 (例如, 使用 SQL Server Management Studio)。

您还可以指定该服务器的服务主体名称 (SPN)。

### <a name="with-active-directory-integrated-authentication"></a>使用 Active Directory 集成身份验证

指定驱动程序使用 Azure Active Directory SQL Server 进行身份验证。 选中后，SQL Server 通过 Azure Active Directory 集成登录安全性使用此数据源来建立连接，而不考虑服务器上的当前登录安全模式。

### <a name="with-sql-server-authentication"></a>使用 SQL Server 身份验证

指定驱动程序使用登录 ID 和密码对 SQL Server 进行身份验证。

### <a name="with-active-directory-password-authentication"></a>使用 Active Directory 密码身份验证

指定驱动程序使用 Azure Active Directory 登录 ID 和密码 SQL Server 进行身份验证。

### <a name="with-active-directory-interactive-authentication"></a>使用 Active Directory 交互式身份验证

通过提供登录 ID 指定驱动程序通过 Azure Active Directory 交互模式 SQL Server 进行身份验证。 这会触发 Windows Azure 身份验证提示对话框。

### <a name="login-id"></a>登录 ID

指定当使用**用户输入的登录 id 和密码进行 SQL Server 身份验证**并使用**用户输入的登录 id 和密码进行 Active Directory 密码身份验证时, 驱动程序用于连接到 SQL SERVER 的登录 id。** 或者, 如果选择了**使用用户输入的登录 ID Active Directory 交互身份验证**, 则为。 这仅适用于为确定服务器默认设置建立的连接；不适用于创建数据源之后使用该数据源建立的后续连接。

### <a name="password"></a>Password

指定在使用**用户输入的登录 id 和密码进行 SQL Server 身份验证**并使用用户输入的**登录 id 和密码进行 Active Directory 密码身份验证时, 驱动程序用于连接到 SQL Server 的密码。** 处于选中状态。 这仅适用于为确定服务器默认设置建立的连接；不适用于使用新数据源建立的后续连接。

如果已选择 "**集成 Windows 身份验证**" 或 "**与 Active Directory 集成身份验证**", 则将禁用 "**登录 ID** " 和 "**密码**" 框。

### <a name="next"></a>Next

继续进入向导的下一屏幕。

### <a name="back"></a>返回

返回到向导的上一个屏幕。

## <a name="next-steps"></a>后续步骤

[数据源向导屏幕 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[数据源向导屏幕 3](../../../connect/odbc/windows/dsn-wizard-3.md)

