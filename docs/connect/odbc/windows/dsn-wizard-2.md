---
title: 数据源向导屏幕 2 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-jizho2
ms.openlocfilehash: e2e6b323428b1ad8ae188ea65bf10382651d3d71
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928247"
---
# <a name="data-source-wizard-screen-2"></a>数据源向导屏幕 2

指定身份验证方法，并设置 Microsoft SQL Server 高级客户端条目，以及适用于 SQL Server 的 ODBC 驱动程序在配置数据源时用于连接到 SQL Server 的登录名和密码。

## <a name="options"></a>选项

### <a name="with-integrated-windows-authentication"></a>使用集成 Windows 身份验证

指定驱动程序请求建立与 SQL Server 之间的安全（或可信）连接。 选中后，SQL Server 将使用集成登录安全性来建立使用此数据源的连接，而不考虑服务器上的当前登录安全模式。 提供的任何登录 ID 或密码都将忽略。 SQL Server 系统管理员必须将你的 Windows 登录名与 SQL Server 登录 ID 关联起来（例如，通过使用 SQL Server Management Studio）。

您还可以指定该服务器的服务主体名称 (SPN)。

### <a name="with-active-directory-integrated-authentication"></a>使用 Active Directory 集成身份验证

指定驱动程序使用 Azure Active Directory 向 SQL Server 进行身份验证。 选中后，SQL Server 通过 Azure Active Directory 集成登录安全性使用此数据源来建立连接，而不考虑服务器上的当前登录安全模式。

### <a name="with-sql-server-authentication"></a>使用 SQL Server 身份验证

指定驱动程序使用登录 ID 和密码向 SQL Server 进行身份验证。

### <a name="with-active-directory-password-authentication"></a>使用 Active Directory 密码身份验证

指定驱动程序使用 Azure Active Directory 登录 ID 和密码向 SQL Server 进行身份验证。

### <a name="with-active-directory-interactive-authentication"></a>使用 Active Directory 交互式身份验证

指定驱动程序通过提供登录 ID 使用 Azure Active Directory 交互模式向 SQL Server 进行身份验证。 这将触发“Azure 身份验证提示”对话框。

### <a name="login-id"></a>登录 ID

如果选择“使用用户输入的登录 ID 和密码进行 SQL Server 身份验证”  或“使用输入用户的登录 ID 和密码进行 Active Directory 密码身份验证”  或“使用用户输入的登录 ID 进行 Active Directory 交互身份验证”  ，则指定驱动程序连接到 SQL Server 时使用的登录 ID。 这仅适用于为确定服务器默认设置建立的连接；不适用于创建数据源之后使用该数据源建立的后续连接。

### <a name="password"></a>密码

如果选择“使用用户输入的登录 ID 和密码进行 SQL Server 身份验证”  或“使用输入用户的登录 ID 和密码进行 Active Directory 密码身份验证”  ，则指定驱动程序连接到 SQL Server 时使用的密码。 这仅适用于为确定服务器默认设置建立的连接；不适用于使用新数据源建立的后续连接。

如果选择“使用集成 Windows 身份验证”  或“使用 Active Directory 集成身份验证”  ，则禁用“登录 ID”  和“密码”  。

### <a name="next"></a>Next

前进到向导的下一个屏幕。

### <a name="back"></a>后退

返回到向导的上一个屏幕。

## <a name="next-steps"></a>后续步骤

[数据源向导屏幕 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[数据源向导屏幕 3](../../../connect/odbc/windows/dsn-wizard-3.md)

