---
title: SQL Server 登录对话框中 (ODBC) |Microsoft 文档
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: v-jizho2
manager: craigg
ms.openlocfilehash: e60be85d872ec3fd6cfce59d7be689b0e03587c7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-login-dialog-box-odbc"></a>“SQL Server 登录”对话框 (ODBC)

当你调用而无需指定足够的信息供要连接到 SQL Server，ODBC 驱动程序显示的驱动程序的 ODBC 连接**SQL Server 登录名**对话框。

## <a name="options"></a>选项

### <a name="server"></a>Server

你的网络上的 SQL Server 实例的名称。 从列表中，选择一个服务器 \ 实例名称或类型中的服务器 \ 实例名称**服务器**框。 或者，您可以创建客户端计算机使用的服务器别名**SQL Server 配置管理器**，并键入该名称的**服务器**框。

当你使用的同一台计算机作为 SQL Server 时，你可以输入"(local)"。 然后，你可以连接到甚至时运行 SQL Server 的非网络版本的 SQL Server 的本地实例。

有关不同类型的网络的服务器名称的详细信息，请参阅 SQL Server 联机丛书中的 SQL Server 安装文档。

### <a name="authentication-mode"></a>身份验证模式

从以下项之一中选择的身份验证模式：
- **SQL Server**与登录 ID 和密码
- **Windows 集成**使用当前登录的用户帐户的身份验证
- **Active Directory 密码**与登录 ID 和密码
- **Active Directory 集成**使用当前登录的用户帐户的身份验证
- **Active Directory 交互式**登录 ID 的身份验证

请参阅[数据源向导屏幕 2](../../../connect/odbc/windows/dsn-wizard-2.md)有关身份验证模式的详细信息。

### <a name="server-spn"></a>服务器 SPN

如果您使用受信任连接，则可为服务器指定服务主体名称 (SPN)。

### <a name="login-id"></a>登录 ID

指定 SQL Server 或 Azure Active Directory 登录 ID，如果用于连接**身份验证模式**设置为**SQL Server**或**Active Directory 密码**或**Active Directory 交互式**。 否则为**登录 ID**禁用框。

### <a name="password"></a>密码

指定的密码。 如果用于连接的 SQL Server 或 Azure Active Directory 登录 ID**身份验证模式**设置为**SQL Server**或**Active Directory 密码**. 否则为**密码**禁用框。

### <a name="options"></a>选项

显示或隐藏**选项**组。 **选项**会启用按钮**服务器**具有值。

### <a name="change-password"></a>更改密码

如果选中此框，显示**新密码**和**确认新密码**框。

### <a name="new-password"></a>新密码

指定新密码。

### <a name="confirm-new-password"></a>确认新密码

再次指定新密码以便确认。

### <a name="database"></a>数据库

指定将用于该连接的默认数据库。 此设置将覆盖为该服务器上的登录名指定的默认数据库。 如果未指定数据库，连接将使用为该服务器上的登录名指定的默认数据库。

### <a name="mirror-server"></a>镜像服务器

指定要镜像的数据库的故障转移伙伴的名称。

### <a name="mirror-spn"></a>镜像 SPN

您还可以指定镜像服务器的 SPN。 镜像服务器的 SPN 用于在客户端和服务器之间相互进行身份验证。

### <a name="language"></a>语言

指定要用于 SQL Server 系统消息的国家/地区的语言。 运行 SQL Server 的计算机必须安装的语言。 此设置将覆盖为该服务器上的登录名指定的默认语言。 如果未指定语言，连接将使用为该服务器上的登录名指定的默认语言。

### <a name="application-name"></a>应用程序名称

（可选）指定要存储在应用程序名称**program_name**此连接中的行中的列**sys.sysprocesses**。

### <a name="workstation-id"></a>工作站 ID

（可选）指定要存储中的工作站 ID**主机名**此连接中的行中的列**sys.sysprocesses**。

### <a name="use-strong-encryption-for-data"></a>对数据使用强加密

当选中时，将加密数据，通过连接进行传递。 默认情况下，即使清除此复选框，也将对登录名加密。

### <a name="trust-server-certificate"></a>信任服务器证书

此选项是适用时，才**对数据进行强加密**已启用。 当选中时，服务器的证书将不验证服务器的正确的主机名，以及由受信任的证书颁发机构颁发。

## <a name="see-also"></a>另请参阅

[Microsoft ODBC Driver for SQL Server（Windows 平台）](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
