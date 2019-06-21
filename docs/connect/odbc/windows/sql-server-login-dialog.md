---
title: SQL Server 登录对话框 (ODBC) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 2d7cf1f31ce5cf42b9c2e4c7b72938b8def2ed4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797741"
---
# <a name="sql-server-login-dialog-box-odbc"></a>“SQL Server 登录”对话框 (ODBC)

当调用一个 ODBC 连接而不为驱动程序指定足够的信息来连接到 SQL Server 时，ODBC 驱动程序将显示“SQL Server 登录”  对话框。

## <a name="options"></a>选项

### <a name="server"></a>“服务器”

在网络上的 SQL Server 实例的名称。 从列表中选择一个服务器\实例名，或在“服务器”  框中键入服务器\实例名。 或者，可以在客户端计算机上使用“SQL Server 配置管理器”  创建服务器别名，并在“服务器”  框中键入该名称。

当使用与 SQL Server 相同的计算机时可以输入“(local)”。 即使正在运行非联网版的 SQL Server，也可以连接到 SQL Server 的本地实例。

有关不同网络类型的服务器名称的详细信息，请参阅“SQL Server 联机丛书”中的 SQL Server 安装文档。

### <a name="authentication-mode"></a>身份验证模式

从以下项之一中选择的身份验证模式：
- **SQL Server**与登录 ID 和密码
- **Windows 集成**使用当前登录的用户帐户进行身份验证
- **Active Directory 密码**与登录 ID 和密码
- **Active Directory 集成**使用当前登录的用户帐户进行身份验证
- Active Directory 交互式身份验证与登录 ID 

请参阅[数据源向导屏幕 2](../../../connect/odbc/windows/dsn-wizard-2.md)的身份验证模式的详细信息。

### <a name="server-spn"></a>服务器 SPN

如果您使用受信任连接，则可为服务器指定服务主体名称 (SPN)。

### <a name="login-id"></a>登录 ID

指定要用于该连接，如果 SQL Server 或 Azure Active Directory 登录 ID**身份验证模式**设置为**SQL Server**或**Active Directory 密码**或**Active Directory 交互式**。 否则为**登录 ID**框处于禁用状态。

### <a name="password"></a>Password

如果用于连接的 SQL Server 或 Azure Active Directory 登录 id 指定的密码**身份验证模式**设置为**SQL Server**或**Active Directory 密码**. 否则为**密码**框处于禁用状态。

### <a name="options"></a>选项

显示或隐藏“选项”  组。 如果“服务器”具有值，则启用“选项”   按钮。

### <a name="change-password"></a>更改密码

选中此框后，将显示“新密码”和“确认新密码”框   。

### <a name="new-password"></a>新密码

指定新密码。

### <a name="confirm-new-password"></a>确认新密码

再次指定新密码以便确认。

### <a name="database"></a>“数据库”

指定将用于该连接的默认数据库。 此设置将覆盖为该服务器上的登录名指定的默认数据库。 如果未指定数据库，连接将使用为该服务器上的登录名指定的默认数据库。

### <a name="mirror-server"></a>镜像服务器

指定要镜像的数据库的故障转移伙伴的名称。

### <a name="mirror-spn"></a>镜像 SPN

您还可以指定镜像服务器的 SPN。 镜像服务器的 SPN 用于在客户端和服务器之间相互进行身份验证。

### <a name="language"></a>“报表”

指定用于 SQL Server 系统消息的国家/地区语言。 运行 SQL Server 的计算机必须安装该语言。 此设置将覆盖为该服务器上的登录名指定的默认语言。 如果未指定语言，连接将使用为该服务器上的登录名指定的默认语言。

### <a name="application-name"></a>应用程序名称

（可选）指定将要存储在 sys.sysprocesses  中该连接所在行的 program_name  列的应用程序名称。

### <a name="workstation-id"></a>工作站 ID

（可选）指定将要存储在 sys.sysprocesses  中该连接所在行的 hostname  列的工作站 ID。

### <a name="use-strong-encryption-for-data"></a>对数据使用强加密

选中时，通过该连接传递的数据将被加密。 默认情况下，即使清除此复选框，也将对登录名加密。

### <a name="trust-server-certificate"></a>信任服务器证书

此选项才适用时，才**对数据使用强加密**已启用。 选中时，不将验证服务器的证书具有正确的主机名的服务器和受信任的证书颁发机构颁发。

## <a name="see-also"></a>另请参阅

[Microsoft ODBC Driver for SQL Server（Windows 平台）](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
